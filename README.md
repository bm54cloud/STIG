# STIG

### INITIAL SET-UP
Deploy MAAS server

ssh ubuntu@IP_address

sudo apt update && sudo apt upgrade

sudo apt install unzip

### Install OpenSCAP
sudo apt install libopenscap8     

### Install SCAP Security Guide
sudo apt install ssg-debderived    
cd /usr/share/xml/scap/ssg/content

### Download the latest Scap Security Guide to include 20.04
sudo wget https://github.com/ComplianceAsCode/content/releases/download/v0.1.69/scap-security-guide-0.1.69.zip     

### Unzip Scap Security Guide
sudo unzip scap-security-guide-0.1.69.zip
cd scap-security-guide-0.1.69/
ls

### Display a list of available Profiles
oscap info ssg-ubuntu2004-ds-1.2.xml

### Evaluate a STIG Profile and write XCCDF results into a report.html file
sudo oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_stig --report report.html ssg-ubuntu2004-ds-1.2.xml

### Secure copy results file from remote to local in new terminal window
scp ubuntu@10.1.29.82:/usr/share/xml/scap/ssg/content/scap-security-guide-0.1.69/report.html ~/Development
cd ~/Development

# AUTOMATED CLOUD-INIT

### Testing with Multipass VM
multipass launch focal --name STIG --cloud-init cloud-init.yaml # "focal" is Ubuntu 20.04
multipass shell STIG

### Confirm user was created
cat /etc/passwd

### Change to scap_auditor user
sudo -i -u scap_auditor # su scap_auditor asks for a password that is not set up

