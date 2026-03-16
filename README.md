# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program
server.py

```
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()
```
client.py

```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()
```

## Output
server.py

<img width="528" height="272" alt="Screenshot 2026-03-16 091101" src="https://github.com/user-attachments/assets/951443bf-ab85-41f9-b1a7-c48de80b6809" />

client.py

<img width="939" height="681" alt="Screenshot 2026-03-16 091548" src="https://github.com/user-attachments/assets/206be8a1-00c3-4e31-89a4-6b326675e115" />

<img width="955" height="848" alt="Screenshot 2026-03-16 091558" src="https://github.com/user-attachments/assets/6aa5aefb-6d4c-4be4-8167-b5afaddd68ed" />



## Result
Thus Execution of Network commands Performed 
