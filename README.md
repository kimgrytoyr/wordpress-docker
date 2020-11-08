# Wordpress, Docker and phpcs

> **Disclaimer:** This project is meant to be used for development purposes only. It's **not** meant to be used in production.

> It's also work in progress. Feel free to contribute if you have anything useful to add.

---

This is a simple Wordpress Docker image with the following features:

- phpcs and the Wordpress Coding Standard is automatically installed
- Visual Studio Code project settings enable the use of phpcs by default

The package is meant to be used in Visual Studio Code with the Remote-Containers extension.

## Features
- MySQL image and the latest WordPress image – WordPress runs at https://localhost:8000
- PHP code linting and formatting adhering to the WordPress Coding Standard.
- Pre-installed node so that you can use [npx @wordpress/...](https://developer.wordpress.org/block-editor/packages/#using-the-packages-via-npm)

## Usage
1. Open Visual Studio Code.
2. Make sure you have the [Visual Studio Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension installed.
3. Open the command palette and run the command `Remote-Containers: Open Folder in Container`
4. Wait for it...
5. Happy coding!

Thats it! You should now have a database server and Wordpress running in separate containers. Linting and formatting adhering to the WordPress Coding Standard should just work.

Visit your WordPress site at `http://localhost:8000`.

## Adding plugins and themes
If you're developing a plugin or a theme and you have that project locally on your computer, just add them as volumes in the `docker-compose.yml` file below the `wp_root` volume, like this:

```
volumes:
    - wp_root:/var/www/html
    - /opt/dev/awesome-plugin:/var/www/html/wp-content/plugins/awesome-plugin
```

..assuming you have the plugin in the local folder `/opt/dev/awesome-plugin`.