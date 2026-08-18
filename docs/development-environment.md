# Development environment

After updating the system, I installed the tools I use for development and documentation.

## Visual Studio Code

I installed Visual Studio Code because I use it for writing code and editing my documentation.

I downloaded the `.deb` package from the official Visual Studio Code website and installed it using the App Center.

It can also be installed from the terminal:

```bash
sudo apt install ./<file>.deb
````

### Install from the Microsoft repository

Another way is to add the Microsoft repository and install VS Code through APT.

First I installed `wget` and `gpg`:

```bash
sudo apt install wget gpg
```

Then I added the Microsoft signing key:

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc \
| sudo gpg --dearmor -o /usr/share/keyrings/microsoft.gpg
```

Then I added the Microsoft repository:

```bash
echo "code code/add-microsoft-repo boolean true" | sudo debconf-set-selections
```

I updated the package lists:

```bash
sudo apt update
```

And installed Visual Studio Code:

```bash
sudo apt install code
```

To start VS Code from the terminal:

```bash
code
```

The installation completed successfully.

## Git

I installed Git because I use it to manage my projects and push them to GitHub.

Install Git with:

```bash
sudo apt install git
```

After installing it, I can check that it works with:

```bash
git --version
```

### Git from the Git PPA

If I want a newer version of Git than the one provided by Ubuntu, I can use the Git Core PPA.

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

I don't need to use the PPA just to use Git. The normal Ubuntu package is enough for this project.
