# Troubleshooting a Home Internet Access Issue

## Objective

Troubleshoot and resolve a home internet access issue on a Windows 11 laptop by identifying the cause through structured network testing, then applying the fix and verifying internet access.

> **Note:** This project used a purposely created internet access issue on a single device for troubleshooting practice. The issue was isolated to the device to avoid affecting the rest of the household network.

## Environment

- Device: Dell Latitude 7400
- Operating System: Windows 11 Pro
- Network Adapter: Intel(R) Wireless-AC 9560 160MHz
- Network: Home 5 GHz Wi-Fi network
- Router: Hitron CODA-5712
- Tools: Network and Sharing Center, PowerShell, Microsoft Edge, Google Chrome, Mozilla Firefox, MacBook Air, iPhone

<img src="screenshots\Environment\Environment_01.png" width="45%" alt="System information in PowerShell">


## Initial Symptom

- Microsoft Edge could not load the GitHub website and displayed the error message, "github.com’s server IP address could not be found."

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_01.png" width="40%" alt="browser error page">

## Phase 1: Confirm Symptom

- Verified the laptop's network connection in Control Panel > Network and Internet > Network and Sharing Center and confirmed the laptop was connected to the Wi-Fi network.

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_05.png" width="50%" alt="network connection status">

- Attempted to load a few other websites and received the same browser error message, indicating the issue was not limited to a single website.

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_02.png" width="40%" alt="Edge error page">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_03.png" width="40%" alt="Edge error page">

- Attempted to open the same websites in Firefox and Chrome to rule out a browser-specific issue. The same errors occurred in both browsers, indicating the issue was not limited to a particular browser.

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_12.png" width="33%" alt="Firefox error page">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_13.png" width="33%" alt="Firefox error page">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_14.png" width="33%" alt="Firefox error page">

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_09.png" width="33%" alt="Chrome error page">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_10.png" width="33%" alt="Chrome error page">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_11.png" width="33%" alt="Chrome error page">

- Attempted to load github.com on other devices connected to the same network to determine if the issue was network-wide or isolated. Confirmed that other devices were able to access the internet and load websites successfully, indicating the issue only affected the Dell laptop.

<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_06.png" width="55%" alt="successfully loaded webpage">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_07.png" width="20%" alt="successfully loaded webpage">
<img src="screenshots\Phase_1_Confirm_Symptom\Phase1_08.png" width="20%" alt="network connection status">

## Phase 2: Identify Network State

- Ran `ipconfig /all` to review the network adapter configuration and confirmed the laptop had a valid IPv4 address, subnet mask, and default gateway, indicating the device was connected to the local network.

<img src="screenshots\Phase_2_Identify_Network_State\Phase2_01.png" width="40%" alt="ipconfig output">

- Determined the DNS server was set to a local address that wasn't functioning as a DNS server, suggesting a DNS misconfiguration as the likely cause of the issue.

<img src="screenshots\Phase_2_Identify_Network_State\Phase2_02.png" width="40%" alt="DNS server address">

- Continued with connectivity testing to confirm whether the problem was isolated to DNS configuration.

## Phase 3: Test Local Network Connection

- Pinged 127.0.0.1 to verify TCP/IP was responding locally.

<img src="screenshots\Phase_3_Test_Local_Network_Connection\Phase3_01.png" width="35%" alt="loopback ping results">

- Pinged the laptop's assigned IPv4 address to confirm the local IP address was responding.

<img src="screenshots\Phase_3_Test_Local_Network_Connection\Phase3_02.png" width="35%" alt="Laptop address ping results">

- Pinged the default gateway to confirm the laptop could communicate with the router on the local network.

<img src="screenshots\Phase_3_Test_Local_Network_Connection\Phase3_03.png" width="35%" alt="default gateway ping results">

- All tests succeeded, indicating there were no connectivity issues between the laptop and the router.

## Phase 4: Test Internet Connection

- Pinged the public IP 8.8.8.8 to test internet access without using DNS. The address responded, indicating the laptop had internet access and that the issue was likely related to DNS rather than connectivity.

<img src="screenshots\Phase_4_Test_Internet_Connection\Phase4_01.png" width="40%" alt="8.8.8.8 ping results">

## Phase 5: Test Name Resolution

- Pinged `google.com` to test name resolution. The command failed to resolve the hostname.

<img src="screenshots\Phase_5_Test_Name_Resolution\Phase5_01.png" width="50%" alt="ping google.com results">

- Ran `nslookup google.com` to test DNS directly. The lookup failed to return an IP address.

<img src="screenshots\Phase_5_Test_Name_Resolution\Phase5_02.png" width="30%" alt="nslookup google.com results">

- Combined with the successful local network tests from Phase 3 and the successful public IP test from Phase 4, these failed name resolution tests further confirmed the DNS issue identified in Phase 2.

## Phase 6: Resolution

- Opened Network Connections to view the network adapter's IPv4 settings and corrected the DNS configuration by setting the laptop to obtain DNS server addresses automatically.

<img src="screenshots\Phase_6_Resolution\Phase6_01.png" width="45%" alt="network connection settings">

<img src="screenshots\Phase_6_Resolution\Phase6_02.png" width="35%" alt="IPv4 properties">
<img src="screenshots\Phase_6_Resolution\Phase6_03.png" width="35%" alt="IPv4 properties">

- Reconnected to the Wi-Fi network so the updated DNS setting could take effect and the DNS configuration could be refreshed.

## Phase 7: Verify Resolution

- Ran `ipconfig /all` to confirm the DNS server was set correctly and the laptop had a valid IPv4 address, subnet mask, and default gateway. The network adapter showed a valid configuration with a corrected DNS server.

<img src="screenshots\Phase_7_Verify_Resolution\Phase7_01.png" width="50%" alt="ipconfig output">

- Pinged `google.com` to verify that DNS could resolve domain names. The command returned successful replies, confirming DNS resolution was functioning properly.

<img src="screenshots\Phase_7_Verify_Resolution\Phase7_02.png" width="50%" alt="ping google.com results">

- Successfully opened GitHub in Microsoft Edge, confirming internet access had been restored.

<img src="screenshots\Phase_7_Verify_Resolution\Phase7_03.png" width="70%" alt="browser page">

## Results

This project successfully resolved an internet access issue on a Windows 11 laptop. The laptop maintained a connection to the home Wi-Fi network, but incorrect DNS settings prevented it from accessing websites by domain name. Testing confirmed that the laptop could communicate on the local network, which helped isolate the problem to name resolution rather than local network connectivity. After correcting the DNS configuration, internet access was restored and the laptop was able to resolve domain names and load websites.

## Key Takeaways

- DNS misconfiguration can prevent website access even when other network communications are still working.

- Structured testing helps isolate whether the issue is related to local network connectivity, internet access, or name resolution.

- Verifying the fix after making changes helps confirm that internet access has been restored.

## Recommendations

- Document the normal network configuration so unexpected changes are easier to identify later.

- Test a secondary DNS server as a backup option if manual DNS configuration is ever required.

- Create a checklist for diagnosing internet access issues efficiently.
