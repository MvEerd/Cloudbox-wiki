[Plexdrive](https://github.com/dweidenfeld/plexdrive) (by Dominik Weidenfeld) is an app that mounts Google Drive on a server. It works better than others mounting solutions because it caches the stream data for smooth playback of media and and prevention Google Drive API bans. 

_Note: If your server has < 16GB of RAM, give [[this|FAQ#server-ram-is-being-maxed-out]] a read after finishing the steps below._


1. Create a [[Google Drive API Client ID and Client Secret]] for Plexdrive.

    Note: this will be different from the Rclone one. You can use the same Google account; but just create a different project for Plexdrive. 

1. Run this command:

    ```bash
    /opt/plexdrive/plexdrive mount -v 3 --refresh-interval=1m --chunk-check-threads=8 --chunk-load-threads=8 --chunk-load-ahead=4 --max-chunks=100 --fuse-options=allow_other,read_only --config=/opt/plexdrive --cache-file=/opt/plexdrive/cache.bolt /mnt/plexdrive
    ```
1. At "Enter your generated client ID:" paste in the Google API Client ID and press `enter`.

1. At "Enter your generated client secret:", paste in the Google API Client Secret and press `enter`.


   ![](https://i.imgur.com/QSOXgLU.png)

1. Copy the link on the screen  and paste it in your host computer's internet browser. Login with your Google account, if asked, and click `Allow`. You will copy the `authorization code` from your browser, paste it at the prompt, and press `enter`.


   Note 1: You must use the same Google account as the one you are planning to use for Google Drive (see [[Prerequisites| Basics: Prerequisites#4-google-drive-account]]).

   Note 2: If you keep getting the prompt for the authorization code or any other type of error, you might have used an incorrect Client ID/Secret. Remove the `config.json` and `token.json` files from `/opt/plexdrive/` and retry setup.

   - ```
     rm /opt/plexdrive/config.json
     rm /opt/plexdrive/token.json
     ```


   ![](https://i.imgur.com/CJzgkhn.png)


   ![](https://i.imgur.com/eN9pfqo.png)
   
1. When you see `First cache build process started...`, press `ctrl`+`c` on your keyboard to exit.

   ![](http://i.imgur.com/bDTmXbT.png)

    Note: Any errors, such as, `WARNING: Could not get object root from API` or `mount helper error`, means this failed somewhere and you need to figure out why. 

1. Run the following commands (one by one):

    ```bash
    sudo systemctl enable plexdrive
    sudo systemctl start plexdrive
    ```
1. Verify Plexdrive is running ok:

    ```bash
    sudo systemctl status plexdrive
    ```

    You should see it as being `Active: active (running)`.

   ![](https://i.imgur.com/HFihFVO.png)

    ```bash
   plexdrive.service - Plexdrive
   Loaded: loaded (/etc/systemd/system/plexdrive.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2017-10-14 12:41:01 CEST; 8h ago
   Main PID: 1025 (plexdrive)
   Tasks: 21
   Memory: 2.7G
   CPU: 23.494s
   CGroup: /system.slice/plexdrive.service
           └─1025 /opt/plexdrive/plexdrive mount -v 3 --refresh-interval=1m --chunk-check-threads=8 --chunk-load-threads=8 --chunk-
    ```

    If you see an error here, check the [[FAQ|FAQ#plexdrive]] for possible solutions. 

1. After the cache is built (see [[log|Logs#plexdrive]]), all your media files (on the server and on Google Drive - combined) will show up in `/mnt/unionfs/Media/`.

   If your media files are not showing up, then either something went wrong during the setup of Plexdrive (i.e. this page) or your media is not located in the correct folder in Google Drive (see [[Prerequisites| Basics: Prerequisites#4-google-drive-account]] and [[Paths| Basics: Paths#google-drive-paths]]).