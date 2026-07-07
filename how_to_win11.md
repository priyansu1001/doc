# export drivers

- `Export-WindowsDriver -Online -Destination ~\playthings\drivers`
- store it in hdd

# backup and export you data, **yes do it!**
# sync your sign-in's and export them in-case
# copy your `appdata` folder also for your configs
# install-script for all apps using choco
# custom iso using msmg or xml method
#
## ping
it did, stabilized (didnt reduce) my ping 
Open a command prompt with administrator privileges.
Type `ping google.com -f -l 1500`

if you're getting packet loss reports, lower the 1500 value by increments of 50 until you get 0% packet loss, and then increase by increments of 10 until you find your maximum stable MTU.

Open a command prompt with administrator privileges.

   - Type `netsh interface ipv4 show subinterface`
   - Press Enter.
   - You will see a list of network interfaces.
   - Type `netsh interface ipv4 set subinterface “Local Area Connection” mtu=1458 store=persistent` 
You should replace `Local Area Connection` with the name that appeared in the “Interface” (Wifi or Ethernet) and `1458` with your optimal one

just do this also,
make a key -`Psched`
here - `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\`
make a Dword value 0 under it
- `NonBestEffortLimit`
