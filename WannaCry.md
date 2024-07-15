### What is the WannaCry Virus?

WannaCry is a type of ransomware that emerged in May 2017. It infects Windows computers, encrypting files and demanding ransom payments in Bitcoin for their release. The ransomware spread rapidly, affecting over 230,000 computers in more than 150 countries. Major organizations like the UK's National Health Service (NHS), FedEx, and Telefónica were among the victims, leading to significant operational disruptions and financial losses estimated at $4 billion globally.

### Key Characteristics of WannaCry

1. **Exploits Used**: WannaCry leveraged two exploits developed by the NSA:
   - **EternalBlue**: This exploit takes advantage of a vulnerability in the Windows Server Message Block (SMB) protocol to propagate the ransomware.
   - **DoublePulsar**: A backdoor implant that allows the ransomware to be installed on compromised systems【16†source】【18†source】.

2. **Rapid Spread**: WannaCry's propagation method, using the EternalBlue exploit, allowed it to spread like a worm across networks, infecting systems without any user interaction【19†source】.

3. **Ransom Demand**: Infected systems displayed a ransom note demanding payment in Bitcoin to decrypt the files. The demanded amounts typically ranged from $300 to $600【18†source】.

### Stopping the Attack

The spread of WannaCry was halted by a security researcher named Marcus Hutchins, who discovered a "kill switch" in the ransomware's code. By registering an unregistered domain that the malware queried, Hutchins effectively stopped the ransomware from executing further, as it interpreted the response from the domain as an indication it was running in a sandbox environment【16†source】【18†source】.

### Attribution and Ongoing Threat

The attack has been attributed to the North Korea-linked Lazarus Group, although some researchers dispute this attribution. Despite the initial version of WannaCry being neutralized, newer versions without the kill switch have emerged, and the threat remains for unpatched systems【16†source】【18†source】.

### Protection Against WannaCry

To protect against ransomware like WannaCry, consider the following steps:

1. **Regular Updates**: Ensure your operating system and software are up-to-date with the latest patches. Microsoft released a patch for the EternalBlue vulnerability before the attack, but many systems remained unpatched【17†source】【19†source】.
2. **Avoid Suspicious Links**: Do not click on links or open attachments in unsolicited emails.
3. **Backup Data**: Regularly back up important data to offline storage to mitigate data loss in case of infection.
4. **Use Security Software**: Employ robust antivirus and anti-ransomware tools, and keep them updated【17†source】【18†source】.

Understanding the mechanics and risks of ransomware like WannaCry is crucial for maintaining cybersecurity and protecting against similar future threats.