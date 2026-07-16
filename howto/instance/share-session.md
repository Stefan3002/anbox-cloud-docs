---
myst:
  html_meta:
    "description": "How to share an active Anbox Cloud streaming session with another user via the Stream Gateway."
---

(howto-share-session)=
# Share a session

A session in Anbox Cloud denotes the streaming session of an Anbox instance. Each session of an instance can be shared up to a maximum of 5 times. By default, each share will expire after 12 hours, with a maximum allowed duration of 30 days per share.

```{note}
This guide demonstrates the steps using the appliance deployment. If you are using the charmed deployment, use `anbox-stream-gateway` instead of `anbox-cloud-appliance.gateway` in the commands.
```

When you have a running instance with streaming enabled, use:

    sudo anbox-cloud-appliance.gateway session share <session_id> --description="share with John Doe"

A share of the session with `<session_id>` is created.

When you have many such shares for various purposes, you may want to update or revoke a session share. To do that, first identify the ID of the share:

    sudo anbox-cloud-appliance.gateway share list --session-id=<session_id>

Notice that the description you provide at the time of creating the share helps in identification.

To update the expiry, run:

    anbox-stream-gateway share update <share_id> --expiry=24h

The `--expiry` flag accepts values in these formats:

- A relative duration such as 24h or 30m, calculated from the current time
- A date-only string in the format `YYYY-MM-DD`
- A date-time string in the format `YYYY-MM-DD HH:MM:SS`

To update the description, run:

    anbox-stream-gateway share update <share_id> --description=new_description

To revoke a share, run:

    anbox-stream-gateway share delete <share_id>

## Sharing a session via the web dashboard

In addition to using the command-line interface, you can now share a session directly from the web dashboard. The *Stream Controls Bar* in the session view includes a **Share Session** button. 

To share a session:

1. Navigate to the session view of the instance you want to share.
2. Locate the **Share Session** button in the *Stream Controls Bar*.
3. Click the **Share Session** button. This will open a dialog where you can configure the share settings, such as the description and expiry time.
4. Confirm the share to generate a share link.

The share link can then be provided to another user, allowing them to access the streaming session.

To stop sharing a session, you can revoke the share link using the **Revoke Share** option in the same dialog.

## Connecting ADB via the web dashboard

The *Stream Controls Bar* also includes a **Connect ADB** button, which allows you to connect to the instance's ADB (Android Debug Bridge) interface directly from the web dashboard.

To connect ADB:

1. Navigate to the session view of the instance you want to connect to.
2. Locate the **Connect ADB** button in the *Stream Controls Bar*.
3. Click the **Connect ADB** button. This will establish an ADB connection to the instance.

If the ADB side panel is already active, the button will indicate its active state. You can disconnect ADB by closing the side panel or clicking the button again.
