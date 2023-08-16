# VSCode DevContainer for nRF Connect SDK


## Initial setup
1. nRF Connect (Ctrl+Alt+N)
2. Open welcome page
    - nRF Connect SDK  
    "Browse..." and set `/workdir` to see SDK version
    - nRF Connect Toolchain  
    Toolchan version should be seen

## Example: `hello_world` on `qemu_cortex_m3`
1. nRF Connect (Ctrl+Alt+N)
2. Create a new application
    - Application type: Freestanding
    - nRF Connect SDK: Version could be seen
    - nRF Connect Toolchain: Version could be seen
    - Application location: `/workspace`
    - Application templete:
        - click the box, and type `hello_` to find `zephyr/samples/hello_world`
    - Application name: `hello_world`
3. Click `Create Application`
4. nRF Connect (Ctrl+Alt+N)
    - APPLICATIONS => `hello_world`
    - CLick `Click to create one` to create build configuration
    - **Add Build Configuration**
        - Board: Click `All boards` (`Nordic boards` or `All boards`), type `cortex_m3` in the box, and select `qemu_cortex_m3`
        - Configutation: `prj.conf`
        - Check: `Enable debug options`  
        => Then Click `Build Configuration` => Build starts

### Debug
1. Explorer(Ctrl+Shift+E)
2. Open `hello_world/src/main.c` (Keep active)
3. Debug (Ctrl+Shift+D)
4. Click `create a launch.json file` select `hello_world`, then `C++(GDB/LLDB)`
5. Move the cursor between `[ ]` just after `"configurations"`, and type `C`,  
and choose `C/C++ (gdb) Launch`

6. Edit "program", add "miDebuggerPath" and "miDebuggerServerAddress" as below
    ```json 
    {
        ...
        "program": "${workspaceFolder}/build/zephyr/zephyr.elf",
        ...
        "MIMode": "gdb",
        "miDebuggerPath": "/root/ncs/toolchains/1f9b40e71a/opt/zephyr-sdk/arm-zephyr-eabi/bin/arm-zephyr-eabi-gdb",
        "miDebuggerServerAddress": "localhost:1234",
        "setupCommands": [
        ...
    }

    ```
7. Terminal => New Terminal, and select `hello_world`
8. type below to start debugserver
    ```bash
    while true; do nrfutil toolchain-manager launch -- /bin/sh -c 'ninja debugserver -C build -v' ; done
    ```
9. Open main.c and set breakpoint by clicking the left side of main() function.
10. Press `[F5]` key to start debug


## Note(s)
- `west` command
    1. Terminal => New Terminal
    2. Type:  
    `nrfutil toolchain-manager launch --shell`
