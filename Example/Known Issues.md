# Known Issues

## Known Issues

Since Laravel Sail was first introduced in Laravel 8.X, many modifications have been made to get it working with the `incfile/atomic` repo.

*   When adding/removing composer packages, we must rebuild our containers.

  

### 🐞 Error not running the PDF

When the pdf is not showing by an issue with the atomic-resources file:

  

**Solution**

  

1. Enter the VM:
    1. Using the CMD
        1. With Sail as an alias ➝ `Sail bash`
    2. Using the Docker interface
        1. ![](https://t2403958.p.clickup-attachments.com/t2403958/132d513d-b083-4ed3-9a40-a9bb263b97cb/image.png)
2. Use ➝ `Composer Install`

  

* * *

  

### 🐞 Error "laravel" is not running the container

When navigating, this error appears:

  

![](https://t2403958.p.clickup-attachments.com/t2403958/f4eb8e59-2151-42e4-b95d-d93891f469c9/image.png)

**Solution**

  

1. Go to the composer page: [https://getcomposer.org/download/](https://getcomposer.org/download/) and copy the lines there.
2. Go to this file `atomic/sail/images/phpfpm/Dockerfile` and paste them.

  

* * *

  

### 🐞 Error undefined T\_VARIABLE

  

While executing `composer global require laravel/sail` returns the error: `undefined T_VARIABLE`

  

**Solution**

  

You will require an [installer](https://getcomposer.org/installer) script provided by **Composer**, download and use it to install **Composer**.

  

1. Make sure you're in your home directory, then retrieve the installer using `curl`:

  

```bash
cd ~
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
```

  

1. Verify that the downloaded installer matches the SHA-384 hash for the latest installer found on the [Composer Public Keys / Signatures](https://composer.github.io/pubkeys.html) page. To facilitate the verification step, you can use the following command to obtain the latest hash from the **Composer** page and store it in a shell variable:

  

```plain
HASH=`curl -sS https://composer.github.io/installer.sig`
```

  

1. Execute the following PHP code, as provided in the **Composer** [download page](https://getcomposer.org/download/), to verify that the installation script is safe to run:

  

```plain
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

  

1. The following output will be shown:

  

```plain
Installer verified
```

  

* * *

  

### 🐞 Error got permission denied

  

While executing the `sail up` command shows the error: `got permission denied` 

  

Solution

  

Create the **Docker** group and add your user:

  

1. Create the **Docker** group.

  

```plain
$ sudo groupadd docker
```

  

1. Add your user to the **Docker** group.

  

```plain
$ sudo usermod -aG docker $USER
```

  

1. Sometimes after an upgrade the permission is denied.

  

```plain
sudo chmod 666 /var/run/docker.sock
```

  

* * *

  

### 🐞 Error Response from Daemon

  

If at the end of the sail up shows the error: `Error Response from Daemon. Driver failed programming external connectivity on endpoint nginx` 

  

Solution

  

You may have **apache2** running. You can check it with:

  

```plain
sudo service apache2 status 
```

  

To stop it use:

  

```plain
sudo service apache2 stop
```

  

* * *

  

### 🐞 Error Laravel Declaration

  

While executing the `sail up` command shows the error: `Laravel error Declaration of App\Exceptions\Handler::report(Throwable $exception)` or `packagemanifest.php line 122`

  

Solution

  

1. Delete the Vendors file.
2. Get the package to **_detect_** web **_crawlers_** via the user agent, execute:

  

```plain
composer require jaybizzle/crawler-detect
```

  

1. The report and render methods class should accept the `Throwable` interface instead of `Exception` instances:

  

```plain
use Throwable;

public function report(Throwable $exception);
public function render($request, Throwable $exception);
```

  

1. If the error persists try using the PHP 7.4 version.
    1. Uninstall your version

```plain
sudo apt-get purge php{version}
sudo apt-get autoclean
sudo apt-get autoremove
```

1.     1. Install PHP 7.4

```plain
sudo apt -y install php7.4
```

  

1.     1. Make sure to have these dependencies

```plain
sudo apt-get install -y php7.4-cli php7.4-json php7.4-common php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath php7.4-soap
```

  

* * *

  

### 🐞 Error Grant permission

At the end of the installation trying to access [db.cool](http://db.cool) shows an error "failed to open stream: Permission denied"

  

Solution

In Ubuntu, set permission to the Storage folder:

  

*   `chmod -R 777 storage/`

  

* * *

## Known Issues Windows

### 🐞 Error Grant gpg: no valid OpenGPG data found

If you get this message you may install GPG to continue.

  

Solution

Update apt database and install gpg by running the following command:

  

```plain
 sudo apt-get update

 sudo apt-get -y install gpg
```

  

* * *

  

## Known Issues Testing

### 🐞 while running the Installing incfile/atomic-resources Error

  

```plain
Downloading (failed)    Failed to download incfile/atomic-resources from dist: The "https://api.github.com/repos/incfile/atomic-resources/zipball/8cb6cdc9294d81a3cba93b84301933338249f9a4" file could not be downloaded (HTTP/1.1 404 Not Found)
```

  

You should make sure that your Checkout SSH Keys are correct.

  

1. Go to your CircleCI dashboard and select the project you want to add a user key to.
2. Click on the gear icon located at the top right corner of the page to access project settings.
3. In the left sidebar, select "SSH Keys".
4. Under "User Keys", click on "Add SSH Key".

Review that your CircleCI configuration is correct Private ([https://app.clickup.com/2403958/docs/29bkp-891/29bkp-16365](https://app.clickup.com/2403958/docs/29bkp-891/29bkp-16365)).

  

  

  

  

  

  

* * *

🏠 [Home](example.com)