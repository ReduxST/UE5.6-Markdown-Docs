# Python

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/python-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/python-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:45:19

---

## Python

### Python

| **Setting** | **Description** |
| --- | --- |
| **Startup Scripts** | Array of Python scripts to run at startup. These run before the first Tick after the Engine initializes. |
| **Additional Paths** | Array of additional paths to add to the Python system paths. |
| **Isolate Interpreter Environment** | 
Defines whether the embedded interpreter should run in isolation mode.

In isolation, the standard `PYTHON*` environment variables (`PYTHONPATH`, `PYTHONHOME`, and so on), the script's directory and the user's site-packages directory are ignored by the interpreter.

Enabling this prevents the Engine from crashing because of incompatible software.

Consider disabling this option if you tightly control your Python environment and you're sure everything is compatible.

The `UE_PYTHONPATH` environment variable is added to `sys.path` whether the interpreter runs in isolation mode or not.



 |
| **Advanced** |   |
| **Developer Mode (all users)** | 

Defines whether Developer Mode should be enabled on the Python interpreter for all users of the project.

Setting Developer Mode in the Project Settings will only enable Developer Mode and Python development for this particular project. Enabling Developer Mode in the Editor Preferences will enable developer mode for Python development across all projects that are opened with the editor.

Enabling developer mode has an extra cost at boot time associated with generating the Python stub file, because this file is generated every time you restart the editor. If you don't always develop with Python, enable this setting per project.

This setting also enables extra warnings (for example, for deprecated code) and stub code generation for use with external IDEs.



 |

### Python Remote Execution

| **Setting** | **Description** |
| --- | --- |
| **Enable Remote Execution** | Defines whether remote Python execution should be enabled. |
| **Advanced** |   |
| **Multicast Group Endpoint** | The multicast group endpoint (in the form of `IP_ADDRESS:PORT_NUMBER` that the UDP multicast socket should join). |
| **Multicast Bind Address** | The adapter address that the UDP multicast socket should bind to, or `0.0.0.0` to bind to all adapters. |
| **Send Buffer Size** | Size of the send buffer for the remote endpoint connection. |
| **Receive Buffer Size** | Size of the receive buffer for the remote endpoint connection. |
| **Multicast Time-To-Live** | The TTL that the UDP multicast socket should use (`0` is limited to the local host, `1` is limited to the local subnet). |