
PS C:\Users\Administrator\Downloads\Need for Speed - Most Wanted\Need for Speed - Most Wanted> adb --help
Android Debug Bridge version 1.0.41
Version 35.0.1-11580240
Installed as C:\platform-tools\adb.exe
Running on Windows 10.0.19045

global options:
 -a                       listen on all network interfaces, not just localhost
 -d                       use USB device (error if multiple devices connected)
 -e                       use TCP/IP device (error if multiple TCP/IP devices available)
 -s SERIAL                use device with given serial (overrides $ANDROID_SERIAL)
 -t ID                    use device with given transport id
 -H                       name of adb server host [default=localhost]
 -P                       port of adb server [default=5037]
 -L SOCKET                listen on given socket for adb server [default=tcp:localhost:5037]
 --one-device SERIAL|USB  only allowed with 'start-server' or 'server nodaemon', server will only connect to one USB device, specified by a serial number or USB device address.
 --exit-on-write-error    exit if stdout is closed

general commands:
 devices [-l]             list connected devices (-l for long output)
 help                     show this help message
 version                  show version num

networking:
 connect HOST[:PORT]      connect to a device via TCP/IP [default port=5555]
 disconnect [HOST[:PORT]]
     disconnect from given TCP/IP device [default port=5555], or all
 pair HOST[:PORT] [PAIRING CODE]
     pair with a device for secure TCP/IP communication
 forward --list           list all forward socket connections
 forward [--no-rebind] LOCAL REMOTE
     forward socket connection using:
       tcp:<port> (<local> may be "tcp:0" to pick any open port)
       localabstract:<unix domain socket name>
       localreserved:<unix domain socket name>
       localfilesystem:<unix domain socket name>
       dev:<character device name>
       jdwp:<process pid> (remote only)
       vsock:<CID>:<port> (remote only)
       acceptfd:<fd> (listen only)
 forward --remove LOCAL   remove specific forward socket connection
 forward --remove-all     remove all forward socket connections
 reverse --list           list all reverse socket connections from device
 reverse [--no-rebind] REMOTE LOCAL
     reverse socket connection using:
       tcp:<port> (<remote> may be "tcp:0" to pick any open port)
       localabstract:<unix domain socket name>
       localreserved:<unix domain socket name>
       localfilesystem:<unix domain socket name>
 reverse --remove REMOTE  remove specific reverse socket connection
 reverse --remove-all     remove all reverse socket connections from device
 mdns check               check if mdns discovery is available
 mdns services            list all discovered services

file transfer:
 push [--sync] [-z ALGORITHM] [-Z] LOCAL... REMOTE
     copy local files/directories to device
     --sync: only push files that have different timestamps on the host than the device
     -n: dry run: push files to device without storing to the filesystem
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression
 pull [-a] [-z ALGORITHM] [-Z] REMOTE... LOCAL
     copy files/dirs from device
     -a: preserve file timestamp and mode
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression
 sync [-l] [-z ALGORITHM] [-Z] [all|data|odm|oem|product|system|system_ext|vendor]
     sync a local build from $ANDROID_PRODUCT_OUT to the device (default all)
     -n: dry run: push files to device without storing to the filesystem
     -l: list files that would be copied, but don't copy them
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression

shell:
 shell [-e ESCAPE] [-n] [-Tt] [-x] [COMMAND...]
     run remote shell command (interactive shell if no command given)
     -e: choose escape character, or "none"; default '~'
     -n: don't read from stdin
     -T: disable pty allocation
     -t: allocate a pty if on a tty (-tt: force pty allocation)
     -x: disable remote exit codes and stdout/stderr separation
 emu COMMAND              run emulator console command

app installation (see also `adb shell cmd package help`):
 install [-lrtsdg] [--instant] PACKAGE
     push a single package to the device and install it
 install-multiple [-lrtsdpg] [--instant] PACKAGE...
     push multiple APKs to the device for a single package and install them
 install-multi-package [-lrtsdpg] [--instant] PACKAGE...
     push one or more packages to the device and install them atomically
     -r: replace existing application
     -t: allow test packages
     -d: allow version code downgrade (debuggable packages only)
     -p: partial application install (install-multiple only)
     -g: grant all runtime permissions
     --abi ABI: override platform's default ABI
     --instant: cause the app to be installed as an ephemeral install app
     --no-streaming: always push APK to device and invoke Package Manager as separate steps
     --streaming: force streaming APK directly into Package Manager
     --fastdeploy: use fast deploy
     --no-fastdeploy: prevent use of fast deploy
     --force-agent: force update of deployment agent when using fast deploy
     --date-check-agent: update deployment agent when local version is newer and using fast deploy
     --version-check-agent: update deployment agent when local version has different version code and using fast deploy
     (See also `adb shell pm help` for more options.)
 uninstall [-k] PACKAGE
     remove this app package from the device
     '-k': keep the data and cache directories

debugging:
 bugreport [PATH]
     write bugreport to given PATH [default=bugreport.zip];
     if PATH is a directory, the bug report is saved in that directory.
     devices that don't support zipped bug reports output to stdout.
 jdwp                     list pids of processes hosting a JDWP transport
 logcat                   show device log (logcat --help for more)

security:
 disable-verity           disable dm-verity checking on userdebug builds
 enable-verity            re-enable dm-verity checking on userdebug builds
 keygen FILE
     generate adb public/private key; private key stored in FILE,

scripting:
 wait-for[-TRANSPORT]-STATE...
     wait for device to be in a given state
     STATE: device, recovery, rescue, sideload, bootloader, or disconnect
     TRANSPORT: usb, local, or any [default=any]
 get-state                print offline | bootloader | device
 get-serialno             print <serial-number>
 get-devpath              print <device-path>
 remount [-R]
      remount partitions read-write. if a reboot is required, -R will
      will automatically reboot the device.
 reboot [bootloader|recovery|sideload|sideload-auto-reboot]
     reboot the device; defaults to booting system image but
     supports bootloader and recovery too. sideload reboots
     into recovery and automatically starts sideload mode,
     sideload-auto-reboot is the same but reboots after sideloading.
 sideload OTAPACKAGE      sideload the given full OTA package
 root                     restart adbd with root permissions
 unroot                   restart adbd without root permissions
 usb                      restart adbd listening on USB
 tcpip PORT               restart adbd listening on TCP on PORT

internal debugging:
 start-server             ensure that there is a server running
 kill-server              kill the server if it is running
 reconnect                kick connection from host side to force reconnect
 reconnect device         kick connection from device side to force reconnect
 reconnect offline        reset offline/unauthorized devices to force reconnect

usb:
 attach                   attach a detached USB device
 detach                   detach from a USB device to allow use by other processes
environment variables:
 $ADB_TRACE
     comma/space separated list of debug info to log:
     all,adb,sockets,packets,rwx,usb,sync,sysdeps,transport,jdwp
 $ADB_VENDOR_KEYS         colon-separated list of keys (files or directories)
 $ANDROID_SERIAL          serial number to connect to (see -s)
 $ANDROID_LOG_TAGS        tags to be used by logcat (see logcat --help)
 $ADB_LOCAL_TRANSPORT_MAX_PORT max emulator scan port (default 5585, 16 emus)
 $ADB_MDNS_AUTO_CONNECT   comma-separated list of mdns services to allow auto-connect (default adb-tls-connect)

Online documentation: https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/main/docs/user/adb.1.md

PS C:\Users\Administrator\Downloads\Need for Speed - Most Wanted\Need for Speed - Most Wanted>

255|SHARP1:/ $ pm -h
Package manager (package) commands:
  help
    Print this help text.

  path [--user USER_ID] PACKAGE
    Print the path to the .apk of the given PACKAGE.

  dump PACKAGE
    Print various system state associated with the given PACKAGE.

  list features
    Prints all features of the system.

  has-feature FEATURE_NAME [version]
    Prints true and returns exit status 0 when system has a FEATURE_NAME,
    otherwise prints false and returns exit status 1

  list instrumentation [-f] [TARGET-PACKAGE]
    Prints all test packages; optionally only those targeting TARGET-PACKAGE
    Options:
      -f: dump the name of the .apk file containing the test package

  list libraries
    Prints all system libraries.

  list packages [-f] [-d] [-e] [-s] [-3] [-i] [-l] [-u] [-U]
      [--uid UID] [--user USER_ID] [FILTER]
    Prints all packages; optionally only those whose name contains
    the text in FILTER.  Options are:
      -f: see their associated file
      -d: filter to only show disabled packages
      -e: filter to only show enabled packages
      -s: filter to only show system packages
      -3: filter to only show third party packages
      -i: see the installer for the packages
      -l: ignored (used for compatibility with older releases)
      -U: also show the package UID
      -u: also include uninstalled packages
      --uid UID: filter to only show packages with the given UID
      --user USER_ID: only list packages belonging to the given user

  list permission-groups
    Prints all known permission groups.

  list permissions [-g] [-f] [-d] [-u] [GROUP]
    Prints all known permissions; optionally only those in GROUP.  Options are:
      -g: organize by group
      -f: print all information
      -s: short summary
      -d: only list dangerous permissions
      -u: list only the permissions users will see

  resolve-activity [--brief] [--components] [--user USER_ID] INTENT
    Prints the activity that resolves to the given INTENT.

  query-activities [--brief] [--components] [--user USER_ID] INTENT
    Prints all activities that can handle the given INTENT.

  query-services [--brief] [--components] [--user USER_ID] INTENT
    Prints all services that can handle the given INTENT.

  query-receivers [--brief] [--components] [--user USER_ID] INTENT
    Prints all broadcast receivers that can handle the given INTENT.

  install [-lrtsfdg] [-i PACKAGE] [--user USER_ID|all|current]
       [-p INHERIT_PACKAGE] [--install-location 0/1/2]
       [--originating-uri URI] [---referrer URI]
       [--abi ABI_NAME] [--force-sdk]
       [--preload] [--instantapp] [--full] [--dont-kill]
       [--force-uuid internal|UUID] [--pkg PACKAGE] [-S BYTES] [PATH|-]
    Install an application.  Must provide the apk data to install, either as a
    file path or '-' to read from stdin.  Options are:
      -l: forward lock application
      -R: disallow replacement of existing application
      -t: allow test packages
      -i: specify package name of installer owning the app
      -s: install application on sdcard
      -f: install application on internal flash
      -d: allow version code downgrade (debuggable packages only)
      -p: partial application install (new split on top of existing pkg)
      -g: grant all runtime permissions
      -S: size in bytes of package, required for stdin
      --user: install under the given user.
      --dont-kill: installing a new feature split, don't kill running app
      --originating-uri: set URI where app was downloaded from
      --referrer: set URI that instigated the install of the app
      --pkg: specify expected package name of app being installed
      --abi: override the default ABI of the platform
      --instantapp: cause the app to be installed as an ephemeral install app
      --full: cause the app to be installed as a non-ephemeral full app
      --install-location: force the install location:
          0=auto, 1=internal only, 2=prefer external
      --force-uuid: force install on to disk volume with given UUID
      --force-sdk: allow install even when existing app targets platform
          codename but new one targets a final API level

  install-create [-lrtsfdg] [-i PACKAGE] [--user USER_ID|all|current]
       [-p INHERIT_PACKAGE] [--install-location 0/1/2]
       [--originating-uri URI] [---referrer URI]
       [--abi ABI_NAME] [--force-sdk]
       [--preload] [--instantapp] [--full] [--dont-kill]
       [--force-uuid internal|UUID] [--pkg PACKAGE] [-S BYTES]
    Like "install", but starts an install session.  Use "install-write"
    to push data into the session, and "install-commit" to finish.

  install-write [-S BYTES] SESSION_ID SPLIT_NAME [PATH|-]
    Write an apk into the given install session.  If the path is '-', data
    will be read from stdin.  Options are:
      -S: size in bytes of package, required for stdin

  install-commit SESSION_ID
    Commit the given active install session, installing the app.

  install-abandon SESSION_ID
    Delete the given active install session.

  set-install-location LOCATION
    Changes the default install location.  NOTE this is only intended for debugging;
    using this can cause applications to break and other undersireable behavior.
    LOCATION is one of:
    0 [auto]: Let system decide the best location
    1 [internal]: Install on internal device storage
    2 [external]: Install on external media

  get-install-location
    Returns the current install location: 0, 1 or 2 as per set-install-location.

  move-package PACKAGE [internal|UUID]

  move-primary-storage [internal|UUID]

  pm uninstall [-k] [--user USER_ID] [--versionCode VERSION_CODE] PACKAGE [SPLIT]
    Remove the given package name from the system.  May remove an entire app
    if no SPLIT name is specified, otherwise will remove only the split of the
    given app.  Options are:
      -k: keep the data and cache directories around after package removal.
      --user: remove the app from the given user.
      --versionCode: only uninstall if the app has the given version code.

  clear [--user USER_ID] PACKAGE
    Deletes all data associated with a package.

  enable [--user USER_ID] PACKAGE_OR_COMPONENT
  disable [--user USER_ID] PACKAGE_OR_COMPONENT
  disable-user [--user USER_ID] PACKAGE_OR_COMPONENT
  disable-until-used [--user USER_ID] PACKAGE_OR_COMPONENT
  default-state [--user USER_ID] PACKAGE_OR_COMPONENT
    These commands change the enabled state of a given package or
    component (written as "package/class").

  hide [--user USER_ID] PACKAGE_OR_COMPONENT
  unhide [--user USER_ID] PACKAGE_OR_COMPONENT

  suspend [--user USER_ID] TARGET-PACKAGE
    Suspends the specified package (as user).

  unsuspend [--user USER_ID] TARGET-PACKAGE
    Unsuspends the specified package (as user).

  grant [--user USER_ID] PACKAGE PERMISSION
  revoke [--user USER_ID] PACKAGE PERMISSION
    These commands either grant or revoke permissions to apps.  The permissions
    must be declared as used in the app's manifest, be runtime permissions
    (protection level dangerous), and the app targeting SDK greater than Lollipop MR1.

  reset-permissions
    Revert all runtime permissions to their default state.

  set-permission-enforced PERMISSION [true|false]

  get-privapp-permissions TARGET-PACKAGE
    Prints all privileged permissions for a package.

  get-privapp-deny-permissions TARGET-PACKAGE
    Prints all privileged permissions that are denied for a package.

  get-oem-permissions TARGET-PACKAGE
    Prints all OEM permissions for a package.

  set-app-link [--user USER_ID] PACKAGE {always|ask|never|undefined}
  get-app-link [--user USER_ID] PACKAGE

  trim-caches DESIRED_FREE_SPACE [internal|UUID]
    Trim cache files to reach the given free space.

  create-user [--profileOf USER_ID] [--managed] [--restricted] [--ephemeral]
      [--guest] USER_NAME
    Create a new user with the given USER_NAME, printing the new user identifier
    of the user.

  remove-user USER_ID
    Remove the user with the given USER_IDENTIFIER, deleting all data
    associated with that user

  set-user-restriction [--user USER_ID] RESTRICTION VALUE

  get-max-users

  get-max-running-users

  compile [-m MODE | -r REASON] [-f] [-c] [--split SPLIT_NAME]
          [--reset] [--check-prof (true | false)] (-a | TARGET-PACKAGE)
    Trigger compilation of TARGET-PACKAGE or all packages if "-a".  Options are:
      -a: compile all packages
      -c: clear profile data before compiling
      -f: force compilation even if not needed
      -m: select compilation mode
          MODE is one of the dex2oat compiler filters:
            assume-verified
            extract
            verify
            quicken
            space-profile
            space
            speed-profile
            speed
            everything
      -r: select compilation reason
          REASON is one of:
            first-boot
            boot
            install
            bg-dexopt
            ab-ota
            inactive
            shared
      --reset: restore package to its post-install state
      --check-prof (true | false): look at profiles when doing dexopt?
      --secondary-dex: compile app secondary dex files
      --split SPLIT: compile only the given split name

  force-dex-opt PACKAGE
    Force immediate execution of dex opt for the given PACKAGE.

  bg-dexopt-job
    Execute the background optimizations immediately.
    Note that the command only runs the background optimizer logic. It may
    overlap with the actual job but the job scheduler will not be able to
    cancel it. It will also run even if the device is not in the idle
    maintenance mode.

  reconcile-secondary-dex-files TARGET-PACKAGE
    Reconciles the package secondary dex files with the generated oat files.

  dump-profiles TARGET-PACKAGE
    Dumps method/class profile files to
    /data/misc/profman/TARGET-PACKAGE.txt

  snapshot-profile TARGET-PACKAGE [--code-path path]
    Take a snapshot of the package profiles to
    /data/misc/profman/TARGET-PACKAGE[-code-path].prof
    If TARGET-PACKAGE=android it will take a snapshot of the boot image

  set-home-activity [--user USER_ID] TARGET-COMPONENT
    Set the default home activity (aka launcher).

  set-installer PACKAGE INSTALLER
    Set installer package name

  get-instantapp-resolver
    Return the name of the component that is the current instant app installer.

  set-harmful-app-warning [--user <USER_ID>] <PACKAGE> [<WARNING>]
    Mark the app as harmful with the given warning message.

  get-harmful-app-warning [--user <USER_ID>] <PACKAGE>
    Return the harmful app warning message for the given app, if present

  uninstall-system-updates
    Remove updates to all system applications and fall back to their /system version.

<INTENT> specifications include these flags and arguments:
    [-a <ACTION>] [-d <DATA_URI>] [-t <MIME_TYPE>]
    [-c <CATEGORY> [-c <CATEGORY>] ...]
    [-n <COMPONENT_NAME>]
    [-e|--es <EXTRA_KEY> <EXTRA_STRING_VALUE> ...]
    [--esn <EXTRA_KEY> ...]
    [--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE> ...]
    [--ei <EXTRA_KEY> <EXTRA_INT_VALUE> ...]
    [--el <EXTRA_KEY> <EXTRA_LONG_VALUE> ...]
    [--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE> ...]
    [--eu <EXTRA_KEY> <EXTRA_URI_VALUE> ...]
    [--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>]
    [--eia <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
        (mutiple extras passed as Integer[])
    [--eial <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
        (mutiple extras passed as List<Integer>)
    [--ela <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
        (mutiple extras passed as Long[])
    [--elal <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
        (mutiple extras passed as List<Long>)
    [--efa <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
        (mutiple extras passed as Float[])
    [--efal <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
        (mutiple extras passed as List<Float>)
    [--esa <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (mutiple extras passed as String[]; to embed a comma into a string,
         escape it using "\,")
    [--esal <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (mutiple extras passed as List<String>; to embed a comma into a string,
         escape it using "\,")
    [-f <FLAG>]
    [--grant-read-uri-permission] [--grant-write-uri-permission]
    [--grant-persistable-uri-permission] [--grant-prefix-uri-permission]
    [--debug-log-resolution] [--exclude-stopped-packages]
    [--include-stopped-packages]
    [--activity-brought-to-front] [--activity-clear-top]
    [--activity-clear-when-task-reset] [--activity-exclude-from-recents]
    [--activity-launched-from-history] [--activity-multiple-task]
    [--activity-no-animation] [--activity-no-history]
    [--activity-no-user-action] [--activity-previous-is-top]
    [--activity-reorder-to-front] [--activity-reset-task-if-needed]
    [--activity-single-top] [--activity-clear-task]
    [--activity-task-on-home] [--activity-match-external]
    [--receiver-registered-only] [--receiver-replace-pending]
    [--receiver-foreground] [--receiver-no-abort]
    [--receiver-include-background]
    [--selector]
    [<URI> | <PACKAGE> | <COMPONENT>]
255|SHARP1:/ $ pm list features
feature:reqGlEsVersion=0x30002
feature:android.hardware.audio.low_latency
feature:android.hardware.audio.output
feature:android.hardware.bluetooth
feature:android.hardware.bluetooth_le
feature:android.hardware.camera
feature:android.hardware.camera.any
feature:android.hardware.camera.autofocus
feature:android.hardware.camera.capability.manual_post_processing
feature:android.hardware.camera.flash
feature:android.hardware.camera.front
feature:android.hardware.faketouch
feature:android.hardware.fingerprint
feature:android.hardware.location
feature:android.hardware.location.gps
feature:android.hardware.location.network
feature:android.hardware.microphone
feature:android.hardware.opengles.aep
feature:android.hardware.ram.normal
feature:android.hardware.screen.landscape
feature:android.hardware.screen.portrait
feature:android.hardware.sensor.accelerometer
feature:android.hardware.sensor.light
feature:android.hardware.sensor.proximity
feature:android.hardware.telephony
feature:android.hardware.telephony.gsm
feature:android.hardware.touchscreen
feature:android.hardware.touchscreen.multitouch
feature:android.hardware.touchscreen.multitouch.distinct
feature:android.hardware.touchscreen.multitouch.jazzhand
feature:android.hardware.usb.accessory
feature:android.hardware.usb.host
feature:android.hardware.vulkan.compute
feature:android.hardware.vulkan.version=4194307
feature:android.hardware.wifi
feature:android.hardware.wifi.direct
feature:android.software.activities_on_secondary_displays
feature:android.software.adoptable_storage
feature:android.software.app_widgets
feature:android.software.autofill
feature:android.software.backup
feature:android.software.companion_device_setup
feature:android.software.cts
feature:android.software.home_screen
feature:android.software.input_methods
feature:android.software.managed_users
feature:android.software.midi
feature:android.software.picture_in_picture
feature:android.software.print
feature:android.software.verified_boot
feature:android.software.voice_recognizers
feature:android.software.webview
feature:com.eastaeon.hardware.display.camera_notch
feature:com.google.android.feature.GMSEXPRESS_PLUS_BUILD
feature:com.google.android.feature.WELLBEING
SHARP1:/ $ pm list features > features.md
/system/bin/sh: can't create features.md: Read-only file system
1|SHARP1:/ $
PS C:\Users\Administrator\Desktop\private-gpt> pm  list packages -d
pm : The term 'pm' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the
spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ pm  list packages -d
+ ~~
    + CategoryInfo          : ObjectNotFound: (pm:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\Administrator\Desktop\private-gpt> adb shell
adb.exe: device offline
PS C:\Users\Administrator\Desktop\private-gpt> adb shell
adb.exe: device offline
PS C:\Users\Administrator\Desktop\private-gpt> adb shell
SHARP1:/ $  pm  list packages -d
package:com.google.android.apps.work.oobconfig
package:com.android.nfc
package:com.google.android.webview
package:com.google.android.videos
SHARP1:/ $ pm list permission-groups
permission group:com.google.android.gms.permission.CAR_INFORMATION
permission group:android.permission-group.CONTACTS
permission group:android.permission-group.PHONE
permission group:android.permission-group.CALENDAR
permission group:android.permission-group.CALL_LOG
permission group:android.permission-group.CAMERA
permission group:com.mediatek.permission-group.EMAIL
permission group:android.permission-group.SENSORS
permission group:com.mediatek.permission-group.WIFI
permission group:android.permission-group.LOCATION
permission group:android.permission-group.STORAGE
permission group:android.permission-group.MICROPHONE
permission group:android.permission-group.SMS
permission group:com.mediatek.permission-group.BT
SHARP1:/ $ pm list permission-groups -d
permission group:com.google.android.gms.permission.CAR_INFORMATION
permission group:android.permission-group.CONTACTS
permission group:android.permission-group.PHONE
permission group:android.permission-group.CALENDAR
permission group:android.permission-group.CALL_LOG
permission group:android.permission-group.CAMERA
permission group:com.mediatek.permission-group.EMAIL
permission group:android.permission-group.SENSORS
permission group:com.mediatek.permission-group.WIFI
permission group:android.permission-group.LOCATION
permission group:android.permission-group.STORAGE
permission group:android.permission-group.MICROPHONE
permission group:android.permission-group.SMS
permission group:com.mediatek.permission-group.BT
SHARP1:/ $







# MEDIATEK

SHARP1:/ $ pm list packages | grep media
package:com.mediatek.gba
package:com.mediatek.ims
package:com.android.providers.media
package:com.mediatek.location.lppe.main
package:com.mediatek.ygps
package:com.mediatek.simprocessor
package:com.mediatek.mms.appservice
package:com.mediatek.engineermode
package:com.mediatek.omacp
package:com.mediatek.wfo.impl
package:com.mediatek.emcamera
package:com.mediatek.mdmlsample
package:com.mediatek.providers.drm
package:com.mediatek.batterywarning
package:com.mediatek
package:com.mediatek.nlpservice
package:com.mediatek.atmwifimeta
package:com.mediatek.calendarimporter
package:com.mediatek.thermalmanager
package:com.mediatek.callrecorder
package:com.mediatek.factorymode
package:com.mediatek.mdmconfig
package:com.mediatek.lbs.em2.ui
package:com.mediatek.location.mtknlp
package:com.mediatek.mtklogger
package:com.mediatek.sensorhub.ui













SHARP1:/ $ pm get-privapp-permissions com.qiku.powerengine
{android.permission.REAL_GET_TASKS, android.permission.BATTERY_STATS, android.permission.PACKAGE_USAGE_STATS, android.permission.WRITE_SECURE_SETTINGS, android.permission.MANAGE_USERS, android.permission.INTERACT_ACROSS_USERS, android.permission.OVERRIDE_WIFI_CONFIG, android.permission.FORCE_STOP_PACKAGES, android.permission.MODIFY_PHONE_STATE}
SHARP1:/ $ pm get-privapp-deny-permissions com.qiku.powerengine
{}
SHARP1:/ $

























PS C:\Users\Administrator> adb reboot
PS C:\Users\Administrator> fastboot flashing get_unlock_ability
< waiting for any device >
PS C:\Users\Administrator> fastboot flashing get_unlock_ability
< waiting for any device >
PS C:\Users\Administrator> fastboot flashing get_unlock_ability
< waiting for any device >
PS C:\Users\Administrator> fastboot flashing get_unlock_ability
(bootloader) unlock_ability = 16777216
OKAY [  0.006s]
Finished. Total time: 0.048s
PS C:\Users\Administrator> fastboot flashing get_unlock_ability
(bootloader) unlock_ability = 16777216
OKAY [  0.005s]
Finished. Total time: 0.006s
PS C:\Users\Administrator> fastboot flashing unlock_critical
(bootloader) Start unlock flow

OKAY [ 44.097s]
Finished. Total time: 44.100s
PS C:\Users\Administrator> fastboot --os-version
C:\platform-tools\fastboot.exe: option requires an argument -- os-version
PS C:\Users\Administrator> fastboot reboot
Rebooting                                          OKAY [  0.001s]
Finished. Total time: 0.023s
PS C:\Users\Administrator>