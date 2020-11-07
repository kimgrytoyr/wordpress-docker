# Wordpress, Docker and phpcs

> **Disclaimer:** This project is meant to be used for development purposes only. It's **not** meant to be used in production.

> It's also work in progress. Feel free to contribute if you have anything useful to add.

---

This is a simple Wordpress Docker image with the following features:

- phpcs and the Wordpress Coding Standard is automatically installed
- Visual Studio Code project settings enable the use of phpcs by default

The package is meant to be used in Visual Studio Code with the Remote-Containers extension.

## Usage
In the root of the project, run the following command:
```
docker-compose up -d
```

This will build the Docker image and launch both a database image and the Wordpress image itself.

When this command finishes you can attach to the remote container in VSCode using the Remote-Containers extension. After doing that, install the `wongjn.php-sniffer` extension in the container only.

Thats it! You should now have a working PHP (WordPress) linter and formatter.

Visit your WordPress site at `http://localhost:8000`.

## Adding plugins and themes
If you're developing a plugin or a theme and you have that project locally on your computer, just add them as volumes in the `docker-compose.yml` file below the `wp_root` volume, like this:

```
volumes:
    - wp_root:/var/www/html
    - /opt/dev/awesome-plugin:/var/www/html/wp-content/plugins/awesome-plugin
```

..assuming you have the plugin in the local folder `/opt/dev/awesome-plugin`.