# Contributing

Thanks for checking out our project! If you find a problem or have an idea, feel free to let us know by following the following guidelines and workflows.

## Pre-requisites

Before making an issue, please ensure that you have set up the projects appropriately with the mentioned dependencies. Please refer to the **Dependencies** and **Running the Project** sections in our [README file](README.md). Please also refer to our [Code of Conduct file](CODE_OF_CONDUCT.md) before contributing to this repository.

## Setting up the project

We develop code in the same [Docker](https://www.docker.com/) container that users run the analysis in to allow consistent usage of software and package versions. As mentioned in our [README file](README.md): install [Docker](https://www.docker.com/), clone the repository, make an ssh key, and download the image before proceeding. Any commands in this page must be ran from the root of the repository.

## Working in the Docker Container

We edit and run the code inside the Docker Container, by connecting Positron to the container via ssh. Your project folder is shared with the container at the `/workspace` directory, so a file you change there changes on your computer too. 

### Before your first connection
1. [Install Positron](https://positron.posit.co/download.html) on your computer. It has a Remote SSH feature which allows the connection to the Docker Container without additional extensions.
2. Refer to the **Running the Project** section in our [README file](README.md), and continue to step 3 after you have ran `docker compose pull`.
3. Check your Git configuration on your computer. The following commands should print your name and your email associated to your GitHub acount. `docker-compose.yml` shares your `~/.gitconfig` with the container, so the commits you make there count as yours.

``` bash
git config --global user.email
```

If it prints nothing, set your name and email with the following commands:

``` bash
git config --global user.email "yourname@example.com"
git config --global user.name "Your Name"
```

### Each time you work on the project
1. In a terminal, making sure you are in the root of the repository, start the container in the background:
``` bash
docker compose up -d
```
2. In Positron, open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows).
3. Type and run **Remote SSH: Show Remote Menu** then pick **Connect to Host**.
4. Type `root@localhost:222` and press Enter. A new Positron window should open for you.
    - If it asks for the platform of the remote host, pick **Linux**.
    - If it asks where you trust the host (a "fingerprint"), click **Continue**.
    - The first time, Positron installs its server inside the container. This may take a few minutes.
5. Open the project folder. The bottom left corner shows `SSH: localhost:2222`, but the Explorer says **No folder opened** and the terminal starts in `/root` which has no project files. That is normal, please continue with the following steps:
    - Click **Open** on the top left corner, then **Open Folder**.
    - Delete what is automatically populated in the path box at the top of your window, and type `/workspace`.
    - Click **OK**, you may have to click **OK** a few times before you proceed.
    - The window will reload, and the Explorer panel should show **WORKSPACE [SSH: LOCALHOST:2222]** with the repository's file structure.
6. Pick the Python interpreter. **Note that you should check this every time you start a container instance.**
    - Click the interpreter button at the top right of the window. The **Running Interpreter Sessions** menu only lists sessions that are already runing.
    - Click **New Console Session** and pick **Python 3.x (uv: dsci-522-predicting-tea-category-from-its-caffeine-level)** with the path `/opt/venv/bin/python`. This is the environment built from `uv.lock`.
    - If this is not in the list of available choices, open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows), type and select **Python: Select Interpreter**, choose **Enter interpreter path**, and type `/opt/venv/bin/python`.
    - To check, run `import sys; print(sys.executable)` in the Console. It should print `/opt/venv/bin/python`. 
7. Make changes in a branch as usual. The terminal, console, and render button all run inside the container.
8. When you are done with changes, close the Positron window, then stop and remove the container in a terminal on your computer with `docker compose down`. 


### If it doesn't connect
- **`~/.ssh/id_ed25519.pub` is a folder:** Docker made it because the key didn't exist yet.
  Run `docker compose down`, delete that folder, make the key
  (see the [README](README.md#usage)), and start again.
- **`~/.gitconfig` is a folder, or Git in the container doesn't know your name:**
  the same thing happened with your Git settings.
  Run `docker compose down`, delete that folder, set your name and email (see above), and start again.
- **It asks for a password:** the container can't see your key.
  Check that your key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.
- **"Remote host identification has changed":** you are using a new image.
  Run `ssh-keygen -R "[localhost]:2222"`, then connect again.
- **GitHub asks you to sign in when you push from the container:**
  sign in once in the browser window Positron opens. Positron remembers it.
- **Linux laptops:** ssh refuses the key because the file belongs to you, not `root`.
  Remove the `#` from the `StrictModes no` line in the `Dockerfile` and push,
  so the workflow publishes a fixed image.
- **Port 2222 is already in use:** change the first `2222` in `docker-compose.yml`
  to another number (e.g. `2223`), and connect to that port instead.

More detail: [Working in a container over ssh with Positron](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/lectures/containers-ssh-positron.html).


## Adding or updating a package
Since adding or updating a package will add a substantial amount of lines to `uv.lock`, we request that changes to packages are created on a separate branch and a separate Pull Request. On this new branch, add the package with:

``` bash
uv add <package>==<version>
```

This pins the version in `pyproject.toml` and updates `uv.lock`. Commit the changed `pyproject.toml` and `uv.lock` together and push them to your branch. GitHub Actions will build and publish a new image on Docker Hub, and commit the new `sha-` tag to the `image:` line in `docker-compose.yml` on your branch. When the workflow finishes, get that commit and download the new image:

``` bash
git pull
docker compose pull
```

Then merge the branch into `main` in a Pull Request.

## Publishing the report

The report on GitHub Pages is a copy of the rendered report in `docs/index.html`. Each time you re-render the report, copy it there again, commit, and push: 

``` bash
cp analysis/tea-category-predictor.html docs/index.html`
```

## Reporting Bugs or Suggesting Changes

If something is not working, please open an Issue in the repository. 
* Be descriptive on what went wrong, what commands you used, and what error you got.
* Your description should be reproducible. We highly recommend trying on a different machine before raising an issue as that will help us and you troubleshoot the error.
* Provide useful screenshots so we can see the directory you're in, the branch name if you are on a branch, and the full error message (including the traceback if applicable). 

If you have a suggestion on how we can improve this project, please open an Issue and provide a short description on the improvement and the files that may be affected by said improvement. Providing us with relevant references or studies will also be greatly appreciated if your improvement is specifically for our analysis results or discussions.

## Contributing Code

If you want to make changes, ensure that your fix has an associated Issue on our repository, and please follow these steps:

1. Create a new branch from an up-to-date version `main`. Do not push directly to `main`.
2. Make sure your branch has a short and descriptive name that describes the update you are working on. 
3. Keep your branches small, this will help us organize changes into manageable bit-sized updates and review workload.
4. Commit your changes with clear commit messages.
5. Test your code and re-render the PDF before creating a pull request.
6. Open a pull request and link the related issue.
7. At least one member of this repository must review and approve your changes before merging into the main repository.

## Using AI

You can use tools like ChatGPT or Claude to help with code writing and/or understanding, or fixing unexpected errors. Please make sure you understand and check the results as you are responsible for the code you put into your branch and pull request. Please mention what tool you used and what you used it for in your pull request description. Opening issues, opening pull requests, reviewing and merging pull requests must be executed by humans, not AI tools.

## Attribution

These contributing guidelines were created with the [Breast Cancer Predictor Project's Contributing Guidelines](https://github.com/UBC-MDS/DSCI_522_project-template-breast-cancer-predictor/tree/main?tab=contributing-ov-file) as a reference.
