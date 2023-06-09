# Day 0 - Creating Your Own Server in the Cloud (but cheaper)

* [Complementary video](https://youtube.com/live/_-6UYOjRIVQ?feature=share)
* [Previous "Day 0" threads](https://www.reddit.com/r/linuxupskillchallenge/search/?q=Day%200&restrict_sr=1)

**READ THIS FIRST!** [HOW THIS WORKS & FAQ](https://www.reddit.com/r/linuxupskillchallenge/comments/qeymzb/please_read_this_first_how_this_works_faq/)

## INTRO

First, you need a server. You can't really learn about administering a remote Linux server without having one of your own - so today we're going to buy one!

Through the magic of Linux and virtualization, it's now possible to get a small Internet server setup almost instantly - and at very low cost. Technically, what you'll be doing is creating and renting a VPS ("Virtual Private Server"). In a datacentre somewhere, a single physical server running Linux will be split into a dozen or more Virtual servers, using the KVM (Kernel-based Virtual Machine) feature that's been part of Linux since early 2007.

In addition to a hosting provider, we also need to choose which "flavour" of Linux to install on our server. If you're new to Linux then the range of "distributions" available can be confusing - but the latest LTS ("Long Term Support") version of Ubuntu Server is a popular choice, and what you'll need for this course.

## Signing up with a VPS

Sign-up is immediate - just provide your email address and a password of your choosing and you're in! To be able to create a VM, however, you may need to provide your credit card information (or other information for billing) in the account section.

### Comparison
| Provider      | Instance Type           | vCPU | Memory | Storage   | Price | Trial Credits  | 
| ------------- | ----------------------- | ---- | ------ | --------- | ----- | -------------- | 
| [Digital Ocean](https://www.digitalocean.com/try/developer-brand) | Basic Plan              | 1    | 1 GB   | 25 GB SSD | $6.00 | $200 / 60 days | 
| [Linode](https://www.linode.com/lp/free-credit-short/)        | Nanode 1GB              | 1    | 1 GB   | 25 GB SSD | $5.00 | $100 / 60 days | 
| [Vultr](https://www.vultr.com/vultr-vs-linode/?promo=LINODE150)         | Cloud Compute - Regular | 1    | 1 GB   | 25 GB SSD | $5.00 | $250 / 30 days |
| [Tiktalik](https://tiktalik.com/en)     | VPS Standard | 2 | 1 GB | 20 GB HDD | ~$2.50 | N/A (pre-paid) |

For more details:
* [Get started with Digital Ocean](https://docs.digitalocean.com/products/getting-started/)
* [Get started with Linode](https://www.linode.com/docs/products/platform/get-started/)

## Create a Virtual Machine 

The process is basically the same for all these VPS, but here some step-by-steps:

### VM with Digital Ocean (or Droplet)

* Choose "Manage, Droplets" from the left-hand sidebar. (a "droplet" is Digital Ocean's cute name for a server!)
* Click on *Create > Droplet*
* **Choose Region**: choose the one closes to you. Be aware that the pricing can change depending on the region.
* **DataCenter**: use the default (it will pick one for you)
* **Choose an image**: Select the image "Ubuntu" and opt for the latest LTS version
* **Choose Size**: Basic Plan (shared CPU) + Regular. Click the option with 1GB Mem / 1 CPU / 25GB SSD Disk
* **Choose Authentication Method**: choose "Password" and type a strong password for the root account.
* *Note that since the server is on the Internet it will be under immediate attack from bots attempting to "brute force" the root password. Make it strong!*
* **Or, if you want to be safer**, choose "SSH Key" and [add a new public key that you created locally](https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/)
* Choose a hostname because the default ones are pretty ugly.
* Create Droplet

### VM with Linode (or Node)

* Click on *Create Linode* (a "linode" is Linode's cute name for a server)
* **Choose an Distribution**: Select the image "Ubuntu" and opt for the latest LTS version
* **Choose Region**: choose the one closest to you. Be aware that the pricing can change depending on the region.
* **Linode Plan**: Shared CPU + Nanode 1GB. This option has 1GB Mem / 1 CPU / 25GB SSD Disk
* **Linode Label**: Choose a hostname because the default ones are pretty ugly.
* **Choose Authentication Method**: on the "Root Password" and type a strong password for the root account.
* *Note that since the server is on the Internet it will be under immediate attack from bots attempting to "brute force" the root password. Make it strong!*
* **And, if you want to be safer**, click "Add An SSH Key" and [add a new public key that you created locally](https://www.linode.com/docs/guides/use-public-key-authentication-with-ssh/)
* Create Linode

### VM with Vultr

* Choose "Products, Instances" from the left-hand sidebar. (no cute names)
* Click on *Deploy Server*
* **Choose Server**: Cloud Compute (Shared vCPU) + Intel Regular Performance
* **Server Location**: choose the one closest to you. Be aware that the pricing can change depending on the region.
* **Server image**: Select the image "Ubuntu" and opt for the latest LTS version
* **Server Size**: Click the option with 1GB Mem / 1 CPU / 25GB SSD Disk
* **SSH Keys**: click "Add New" and [add a new public key that you created locally](https://www.vultr.com/docs/deploy-a-new-server-with-an-ssh-key/)
* *Note that since that there's no option to just authenticate with root password, you will need to create a SSH key.*
* **Server Hostname & Label**: Choose a hostname for your server.
* **Disable** "Auto Backups" and "IPv6". They will not be required for the challenge and are only adding to the bill.
* Deploy Now

### VM with Tiktalik

**NOTE:** Do yourself a favor already - [create](http://articles.tiktalik.com/content/help/how-create-ssh-key/) and [add](https://tiktalik.com/en/panel/#sshkeys) a public SSH key to your Tiktalik account, before creating any new server instances - it's safer and more convenient to use.

* Choose "Instances" from the left-pane, in **COMPUTING** section.
* Click on *+Create new instance*
* **Hostname**: Type in the unique name of your server
* **Image**: Select an operating system image, which will be deployed (installed) on your VPS. (For the purpose of this "alternative" implementation, the latest available "CentOS Linux" stable release is preferred).
* **Size**: Click the option "Standard" (preselected) and scale-up/down your server's RAM size, measured with "*Std Unit*s" - each unit adds 1 GB of RAM, default is "1 Std Unit" / a VPS with 1 GB of RAM
(number of available CPUs for all "Standard" instances is fixed to "2 vCPUs")
* **Hard disk**: Use slider to pick the size of your "Standard" instance's HDD (not SSD), with 5 GB "granularity" - default/min. size is 20 GB (max. selectable size is 1000 GB)
* **Networks**: Select one of 5 available (pub2-pub6) public network segments, from which an IP address will be assigned automatically to your server instance
(or leave the default "Public network" selection - it will pick an IP address range at random from all available segments; sidenote: "+Add network interface" button is currently defunct)
* **SSH key**: Leave the default selection "Without SSH key" if you want your *root* account to use a password (for initial authentication); or select the name of one of available SSH keys, to use it for authentication.
* *Note that "SSH key" option is only visible, if any public key(s) was/were [created](http://articles.tiktalik.com/content/help/how-create-ssh-key/) and [added](https://tiktalik.com/en/panel/#sshkeys) to your account earlier*
* +Create

## Logging in for the first time with console

We are going to access our server using SSH but, if for some reason you get stuck in that part, there is a way to access it using a console:

* Digital Ocean: [Droplet Console](https://docs.digitalocean.com/products/droplets/how-to/connect-with-console/)
* Linode: [LISH Console](https://www.linode.com/docs/products/compute/compute-instances/guides/lish/)
* Vultr: [Web Console](https://www.vultr.com/docs/vultr-web-console-faq/)
* Tiktalik: **noVNC** management console is unavailable at this time

## Remote access via SSH

You should see a "Public IPv4 address" (or similar) entry for your server in account's control panel, this is its unique Internet IP address, and it is how you'll connect to it via SSH (the Secure Shell protocol) - something we'll be covering in the first lesson.

* **Digital Ocean**: Click on *Networking tab > Public Network > Public IPv4 Address*
* **Linode**: Click on *Network tab > IP Addresses > IPv4 - Public*
* **Vultr**: Click on *Settings tab > Public Network > Address*
* **Tiktalik**: Click on *Instances* (the public IPv4 address should be visible next to server's DNS address)

If you are using Windows, download Putty and [follow the instructions to connect](https://blog.livialima.net/putty-basics).
Alternatively, in newer Windows versions (10/11), you can use a built-in SSH client via the CLI (e.g. cmd.exe), as described below.

If you are on Linux or MacOS, open a terminal and run the command:

`ssh username@ip_address`

Or, using the SSH private key, `ssh -i private_key username@ip_address`

Enter your password (or a passphrase, if your SSH key is protected with one)

Voila! You have just accessed your server remotely.

If in doubt, consult the [complementary video](https://youtube.com/live/_-6UYOjRIVQ?feature=share)

## Creating a working admin account

We want to follow the Best Practice of not logging as "root" remotely, so we'll create an ordinary user account, but one with the power to "become root" as necessary, like this:

`adduser snori74`

`usermod -a -G wheel snori74`

(Of course, replace 'snori74' with your name!)

You can also verify the correct group name with e.g. `grep -E '^%[a-z]+' /etc/sudoers` and

`getent group $(grep -Eo '^%[a-z]+' /etc/sudoers | tr -d '%')`

*This* will be the account that you use to login and work with your server. It has been added to the 'wheel' group, which on a CentOS system gives it access to read various logs and to "become root" as required via the _sudo_ command.

To login using your new user, [copy the SSH key from root](https://askubuntu.com/questions/1218023/copying-ssh-key-from-root-to-another-user-on-same-machine/1218026#1218026).

## You are now a sysadmin

Confirm that you can now perform administrative tasks, e.g. by typing:

`sudo -l`

## Updating your OS

As CentOS Linux systems have offcially reached their [EOL (End Of Life)](https://www.centos.org/centos-linux-eol/), updating all installed packages to their newest available versions will require some additional preparation.

First, run:

```bash
sudo sed -i.bak -e 's/^mirrorlist=/#mirrorlist=/g' \
                -e 's|^#baseurl=http://mirror|baseurl=http://vault|g' /etc/yum.repos.d/CentOS-*.repo
```

(this is a single command, split into 2 separate lines for readability)

Then:

`sudo dnf -y update`

Don't worry too much about the output and messages from these commands, but it should be clear whether they succeeded or not. (Reply to any prompts by taking the default option). These commands are how you force the installation of updates on a CentOS Linux system, and only an administrator can do them.

**REBOOT**

When a kernel update is identified in this first check for updates, this is one of the few occasions you will need to reboot your server, so go for it after the update is done:

`sudo reboot now`

Your server is now all set up and ready for the course!

You may also want to [convert](https://centos.org/centos-stream/) your "CentOS Linux" to "CentOS Stream", to constantly keep it most up to date.

This will require running some additional commands to update and upgrade your software:

```bash
sudo dnf -y --disablerepo '*' --enablerepo extras swap centos-linux-repos centos-stream-repos
sudo dnf -y distro-sync
sudo reboot now
```

Note that:
* This server is now running, and completely exposed to the whole of the Internet
* You alone are responsible for managing it
* You have just installed the latest updates, so it should be secure for now

To logout, type `logout` or `exit`.

## When you are done

You should be safe running the VM during the month for the challenge, but you can **Stop** the instance at any point. It will continue to count to the bill, though.

When you no longer need the VM, **Terminate/Destroy** instance.

**Now you are ready to start the challenge. Day 1, here we go!**
