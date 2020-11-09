# Wordpress, Docker and phpcs

> **Disclaimer:** This project is meant to be used for development purposes only. It's **not** meant to be used in production.

> It's also work in progress. Feel free to contribute if you have anything useful to add.

---

This is a simple Wordpress Docker image with the following features:

- phpcs and the Wordpress Coding Standard is automatically installed
- Visual Studio Code project settings enable the use of phpcs by default

The package is meant to be used in Visual Studio Code with the Remote-Containers extension.

## Features
- MySQL image
- The latest WordPress image – WordPress runs at https://localhost:8000
- phpMyAdmin – runs at http://localhost:8080
- PHP code linting and formatting adhering to the WordPress Coding Standard.
- Pre-installed node so that you can use [npx @wordpress/...](https://developer.wordpress.org/block-editor/packages/#using-the-packages-via-npm)
- Xdebug automatically configured and ready to use. See below for Xdebug instructions.

## Usage
1. Open Visual Studio Code.
2. Make sure you have the [Visual Studio Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension installed.
3. Open the command palette and run the command `Remote-Containers: Open Folder in Container`
4. Wait for it...
5. Happy coding!

Thats it! You should now have a database server and Wordpress running in separate containers. Linting and formatting adhering to the WordPress Coding Standard should just work. You can also run the default debug configuration using Xdebug.

Visit your WordPress site at http://localhost:8000.

## Debugging with Xdebug
The container has been configured to not run Xdebug when using PHP from the command line. This is to prevent it from being used when PHP-Sniffer is triggered, since it will drastically slow down the linter and the formatter.

Here's how to start a debug session:
1. Launch the debug configuration `Listen for XDebug`
2. In the «Ports» pane in «Remote Explorer», enable forwarding of port `9000` (click the refresh arrow to make it appear)
3. Enable breakpoints and have fun!

> **Note:** When you stop the debugging session, make sure to disable forwarding of port `9000`, or else the page will appear to hang.

## Adding plugins and themes
If you're developing a plugin or a theme and you have that project locally on your computer, just add them as volumes in the `docker-compose.yml` file below the `wp_root` volume, like this:

```
volumes:
    - wp_root:/var/www/html
    - /opt/dev/awesome-plugin:/var/www/html/wp-content/plugins/awesome-plugin
```

..assuming you have the plugin in the local folder `/opt/dev/awesome-plugin`.