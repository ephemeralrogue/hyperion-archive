<h1 align="center">Hyperion Archive</h1>

<p align="center">
    <br>
    <img
        src="../assets/hyperion-archive-emblem.png" 
        alt="hyperion-archive-emblem"
        width="120px"
    />
    <br>
    <br>
    <i>
        ephemeralrogue.bookworm is an Ansible collection written to provision
        <br> Debian Bookworm virtual machines locally.
    </i>
    <br>
</p>

<p align="center">
    <a href="https://anythingllm.com/">AnythingLLM</a>
    •
    <a href="https://ollama.com/">Ollama</a>
    •
    <a href="https://discord.gg/nh7mqGEfbw">{ e } Discord</a>
    •
    <a href="https://blog.ephemeralrogue.xyz/detour-through-ansible#heading-ephemeralroguebookworm">Project Writeup</a>
    <br>
</p>
<hr>
<br>

The Hyperion Archive is a simple [AnythingLLM] setup using [Ollama] as the NLP 
provider. The app runs via [Docker Compose], spinning up both the 
[Ollama container] and the [AnythingLLM container] and linking them for ease 
of setup. The app is designed to be entirely contained within the directory 
the compose file exists.

<a id='contents'></a>
## Contents

- [Running the Docker Compose File](#compose)
- [Setting Up a Systemd Service](#systemd)
- [Future Considerations](#future)

<a id='compose'></a>
## Running the Docker Compose File

To run the enclosed Docker Compose file, follow these steps:

1. **Navigate to the project directory and clone this repository:**
    ```sh
    git clone https://github.com/ephemeralrogue/hyperion-archive.git
    ```

2. **Enter the cloned directory:**
    ```sh
    cd hyperion-archive
    ```

3. **Rename `.env.template` to `.env` and fill in the details.**
    Set the `STORAGE_LOCATION`. You can leave all the other fields alone. If 
    you run into issues where settings are being saved appropriately, you may 
    need to adjust permissions for the `.env` file. Once AnythingLLM saves 
    what it needs to save, return permissions and reset `STORAGE_LOCATION`.

3. **Run Docker Compose:**
    ```sh
    docker compose up -d # if using standalone binary, use docker-compose up -d
    ```

    This command will start the services defined in `compose.yaml` in detached mode.

4. **Open a browser window and navigate to `localhost:3001`**
    You should be greeted by the AnythingLLM app ready to go and already 
    configured to use Ollama. It may take a few minutes for AnythingLLM to 
    recognize Ollama. You may need to manually load a model into Ollama. 
    If so, first check to make sure Ollama is running by navigating to 
    `localhost:11434` in a browser window. If you see "Ollama is running" 
    return to the terminal and run:
    ```sh
    docker exec -it ollama ollama run llama3.2
    ```
    This will load the llama3.2 model. You can change this to any model 
    supported by Ollama. Once the model is loaded, you can return to 
    AnythingLLM. You should be able to create agents after a few minutes.

5. **When finished, shut down the service:**
    ```sh
    docker compose down # or docker-compose down
    ```

[Back to Contents](#contents)

<a id='systemd'></a>
## Setting Up a Systemd Service

If you are running this app on a Linux distro that ships with systemd, you 
can use the included service template in the systemd directory to set up a 
systemd service. This way, you can avoid having to navigate to the project 
directory every time you want to spin up the app. Simply setup the service, 
start the service when you want to use the app, and stop the service when 
you want to shut it down. A README is included in the systemd directory to 
help you set this up.

[Back to Contents](#contents)

<a id='future'></a>
## Future Considerations

As more NLP tools become available and more accessible, this project 
will likely expand with additional services and use-cases.

[Back to Contents](#contents)

<!-- links section -->
[AnythingLLM]: https://anythingllm.com/
[Ollama]: https://ollama.com/
[Docker Compose]: https://docs.docker.com/compose/
[Ollama container]: https://github.com/ollama/ollama/blob/main/docs/docker.md#amd-gpu
[AnythingLLM container]: https://docs.anythingllm.com/installation-docker/local-docker

