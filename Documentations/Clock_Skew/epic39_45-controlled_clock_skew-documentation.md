### Sprint 3 Analytical Report: Clock-Skew Demonstration & Timestamp Correlation Guidance 

1. Epic 39: Controlled Clock-Skew Demonstration & Results

### Phase 1: Baseline Synchronized State
Target Device: RTR-INT-01
Reference Time Source: 10.20.50.20 (SRV-NTP)
Observed State:
show ntp status confirmed: Clock is synchronized, stratum 2, reference is 10.20.50.10 (polling the NTP server network).
show clock displayed: 14:22:13 UTC Sat Oct 10 2026.
Finding: Baseline logs arriving at SRV-SYSLOG on 10.20.50.10 maintained a unified, accurate timeline aligned across all distributed infrastructure.

### Phase 2: Controlled Clock Skew
Methodology: I ran a manual override command clock set 16:00:00 Oct 10 2026..
What I Observed:
show ntp status immediately changed to: Clock is unsynchronized, stratum 16, no reference clock.
show clock updated and kept the skewed time: 16:02:57 UTC Sat Oct 10 2026.
Overall Finding: Manual time entry successfully changed the router from the centralized NTP server, forcing it into an isolated state (Stratum 16) where local drift or forced distortion is preserved independently of the master clock.

### Phase 3: Synchronization Restoration & Recovery
Methodology: Put the configuration bacon for the directive ntp server 10.20.50.20 using global configuration mode.
What I Observed: show ntp status recovered to Clock is synchronized, stratum 2, reference is 10.20.50.10 and show clock re-synchronized back to 14:29:01.
Overall Finding: Recovery is automatic upon returning the NTP server association which eliminates time divergence.

2. Epic 45: Timestamp Correlation Analysis & Impact
Effect on Event Ordering & Reconstruction
When a network device experiences clock skew or drops to Stratum 16 its local system clock changes by itself. When doing incident reconstruction analysts rely heavily on timestamps to sequence logs from multiple sources in cybersecurity this can be done when correlating firewall drops, router config audits, and server access logs.
Concrete Example: If an administrator executes a configuration change (%SYS-5-CONFIG_I) while the router's clock is skewed 2 hours forward, a centralized syslog record from that router will display a timestamp ahead of its actual occurrence. When placed side-by-side with a strictly synchronized application server (SRV-APP-01), an analyst reviewing logs sequentially could misinterpret a post-incident remediation step as the initial point of compromise, completely disrupting the attack timeline.
Packet Tracer Simulation Limitations
NTP Daemon Behavior: In the Cisco IOS simulation environment, active NTP configurations strictly police time overrides. This means when a manual clock is set it instantly strips the synchronization status (forcing Stratum 16) but automated polling changes upstream servers upon configuration updates. Real-world physical environments may have gradual hardware changes rather than quick binary jumps.

3. Practical Guidance for Manual Timestamp Correlation
To account for potential time inconsistencies during incident triage analysts must keep in mind this protocol:
Verify NTP Status First: Before comparing logs across devices do a show ntp status and show ntp associations on each source node to verify Stratum levels and check for any synchronization issues.
Normalize Time Zones and Formats: Ensure all logs are converted to a standard reference baseline (such as UTC) to prevent regional or format-based misinterpretations.
Flag Unknown Offsets: If a device's synchronization state cannot be verified (e.g., unreachable NTP server or Stratum 16 status) you should flag its event timestamps as unverified in the incident report rather than assuming it's all normal.
Correlate Beyond Raw Timestamps: Never rely on timestamps in isolation. Validate event sequences using session sequence numbers and looking for authentication success following authentication failure. 
4. Screenshots:
https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/baseline_verification/baseline_sync_rtr-int-01.png
https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/baseline_verification/clock_skew_stratum16.png
https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/baseline_verification/restored_sync_rtr-int-01.png

6. Peer Review and Sign-Off Record- Teammate Reviewer: (Place Name)   Review Date: (date)  Summary of Feedback: 
