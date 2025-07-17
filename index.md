#  My First Honeypot: Catching Fake Attackers with Cowrie on Ubuntu

---

##  Introduction

Hey! I'm starting my journey in cybersecurity and wanted to get some hands-on experience with real tools. So, I decided to build a honeypot using **Cowrie**, an open-source SSH honeypot that logs attacker activity in a fake shell environment.

In this blog post, I’ll walk through exactly how I set it up on **Ubuntu in VirtualBox**, simulated some attacks, and checked the logs — step-by-step with screenshots.

---

##  What I Used

- Ubuntu 22.04 in VirtualBox
- Internet working inside the VM
- Basic terminal knowledge
- Cowrie (SSH honeypot)
- GitHub Pages (for this blog )

---

##  Step 1: Install Dependencies

I opened the terminal and installed the packages needed for Cowrie:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-venv python3-pip libssl-dev libffi-dev build-essential authbind -y
```
Step 2: Clone and Set Up Cowrie
Next, I cloned Cowrie from GitHub and set up the Python environment:

```bash

git clone https://github.com/cowrie/cowrie.git
cd cowrie
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

```
Step 3: Configure Cowrie
I created the configuration file using the default sample:

```bash

cp etc/cowrie.cfg.dist etc/cowrie.cfg
```
By default, Cowrie listens on port 2222, so there’s no need to change anything unless you want to.

Step 4: Start Cowrie
Now I started the honeypot:

```bash
bin/cowrie start

```
If everything is correct, you should see a message indicating Cowrie started successfully.

Step 5: Simulate an SSH Attack
In a second terminal window, I tested the honeypot by connecting to it:

```bash
ssh -p 2222 root@localhost
```
Cowrie accepted fake credentials and dropped me into a fake shell environment.

Then I typed a few common commands:

```bash
ls
whoami
cat /etc/passwd
```
Cowrie doesn’t execute the commands, but it logs them — exactly what we want in a honeypot.

Step 6: View Logs
To see what Cowrie captured, I ran:

```bash

tail -f var/log/cowrie/cowrie.log

```
This showed all login attempts, commands typed, and session info.

Cowrie also logs complete session keystrokes in the TTY folder:

```bash
ls var/lib/cowrie/tty/
cat var/lib/cowrie/tty/[your-session-filename]
```
Step 7: What I Learned
Cowrie gave me a safe, fake system where I could simulate attacks.

I got comfortable reading logs and understanding how attackers behave.

It gave me a real taste of what a SOC analyst might see.

 Step 8: What’s Next?
Here’s what I’m planning next:

Forward Cowrie logs to Splunk or ELK

Try deploying Cowrie on a VPS (safely, with firewalls)

Experiment with other honeypots like T-Pot or Honeyd

Final Thoughts
Setting up Cowrie was my first real hands-on cybersecurity project. It was surprisingly fun and gave me a deeper understanding of how attacks look from the defender’s side.

If you're new to cybersecurity, I highly recommend building your own honeypot — it’s a perfect project for learning and showing off what you can do.

here are some screenshot from the terminal for better understanding 
![WhatsApp Image 2025-07-17 at 02 19 40](https://github.com/user-attachments/assets/d4dd53aa-cb1e-4cf0-a142-2e7fc96ca80f)
![WhatsApp Image 2025-07-17 at 02 19 45](https://github.com/user-attachments/assets/f589fcb4-fa5d-4c94-bd5e-243fd57badc0)
![WhatsApp Image 2025-07-17 at 02 19 45 (1)](https://github.com/user-attachments/assets/d48c61c7-149b-4004-b2a5-e6eb41dc43e2)
![WhatsApp Image 2025-07-17 at 02 19 45 (2)](https://github.com/user-attachments/assets/00423629-900e-4639-9296-b2b2040f4f9d)

Thanks for reading!
pruthviraj patil 

