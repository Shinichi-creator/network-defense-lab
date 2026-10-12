# Lab Report

## Objective

Document simulated attack findings, remediate a demonstrated vulnerability, and compare the test result before and after the change.

## Environment

| System | Address shown in the topology | Role |
| --- | --- | --- |
| vWorkstation | 172.30.0.2 | Windows workstation |
| pfSense | Internal 172.30.0.1; external 202.20.1.1 | Firewall/router |
| TargetLinux01 | 172.40.0.20 | Linux target |
| AttackMonkey01 | 172.40.0.50 | Simulation host |
| AttackLinux01 | 10.0.1.3 | Lab attack host |

The Infection Monkey report also displays a workstation address of 192.168.56.2. This differs from the topology's workstation address; the screenshots alone do not explain that difference. The report's discovery count is a tool-reported total rather than a count of only the named topology nodes.

## 1. Review simulated compromise

The Infection Monkey map shows propagation between lab systems. Its security report records seven discovered machines and four successful breaches. Recommendations include unique, complex passwords and network segmentation. These are report recommendations; the supplied evidence does not show that passwords were changed or that every recommendation was implemented.

The ATT&CK report records remote file transfers, including EICAR artifacts and simulation executables. It recommends intrusion prevention at network boundaries.

## 2. Validate the initial vulnerability

The initial Metasploit screenshot identifies the Apache CGI/Bash Shellshock module and the Linux target. The check reports a vulnerable target. The subsequent test opens a Meterpreter session, and directory listing output shows the CGI directory. This provides evidence of successful exploitation within the provided lab.

## 3. Apply the package change

A version check shows Bash 4.3.0(1)-release. The next screenshot shows installation of the supplied bash_5.0-6ubuntu1_amd64.deb package using dpkg. The output records unpacking and setup. It also says the package was unpacked over the same package version; therefore, the screenshots do not provide a complete package history or a post-installation version check.

## 4. Retest the exploit path

The existing Meterpreter session was closed before retesting. The check then reports that the target is not exploitable. A repeated exploit attempt finishes without creating a session. This is the strongest before-and-after evidence in the submission, supporting mitigation of the tested path after the package change.

## 5. Review endpoint antivirus evidence

ClamAV recursively scanned the working directory, detected eicar.com and eicar_com.zip, and moved both into /home/user/VIRUS. The summary shows 458 scanned files and two detections. These were EICAR test artifacts, not proof of real malware. The scanner warns that its signature database is older than seven days. Moving files to a directory demonstrates relocation; the screenshot does not establish access controls on that directory.

Windows Security separately shows a custom scan of eight files with zero threats and no listed quarantined or allowed threats. This is a limited scan result, not proof that the whole workstation was clean.

## 6. Review firewall changes

The pfSense DMZ page confirms successfully applied changes and shows an empty rule table. The page states that incoming connections on this interface will be blocked until pass rules are added. The screenshot also displays a default administrator password warning. No follow-up connectivity test or administrator password change is shown, so these remain evidence limitations.

## Lessons learned

- Establish a baseline and repeat the same vulnerability test after remediation.
- Close an existing session before using a new session as evidence of exploit success or failure.
- Distinguish tool recommendations from controls actually implemented.
- Interpret antivirus results in terms of scan scope and signature freshness.
- Pair firewall configuration evidence with connectivity testing to confirm intended behavior.

## Outcome

The supplied evidence documents a successful initial lab exploit and an unsuccessful retest after the package change. It also documents attack simulation analysis, EICAR detection and relocation, a limited Windows scan, and applied DMZ firewall changes. No broader security or production-impact claim is made.
