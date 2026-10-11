# 🔍 Naabu + Nmap Recon Automation

A simple Python automation script that combines **Naabu** and **Nmap** to streamline port discovery and service detection during network reconnaissance.

Instead of manually running both tools, this script first discovers open ports using Naabu and then passes those ports to Nmap for further scanning.

## 🚀 Features

- **Automated port discovery** using Naabu.
- **Service and version detection** using Nmap.
- **Target input through the command line.**
- **Dynamic port selection** — Nmap scans only the ports discovered by Naabu.
- **Basic error handling** and output display.

## ⚙️ How It Works

The script follows a simple two-stage workflow:

1. **Input target:** Accepts a target IP address or hostname through command-line arguments.
2. **Port discovery:** Runs Naabu to identify open ports.
3. **Port extraction:** Extracts the discovered port numbers and combines them into a comma-separated list.
4. **Service detection:** Runs Nmap against the discovered ports using service-version detection.
5. **Display results:** Prints the Nmap scan output in the terminal.

```text
       Target IP / Hostname
                |
                v
        +---------------+
        | Python Script |
        +---------------+
                |
                v
        +---------------+
        |     Naabu     |
        | Port Discovery|
        +---------------+
                |
                v
        +---------------+
        | Extract Ports |
        +---------------+
                |
                v
        +---------------+
        |     Nmap      |
        | Service Scan  |
        +---------------+
                |
                v
        +---------------+
        | Display Output|
        +---------------+
```

## 🛠️ Requirements

Make sure the following tools are installed and available in your system's PATH:

- **Python 3**
- **[Naabu](https://github.com/projectdiscovery/naabu)** — port scanning
- **[Nmap](https://nmap.org/)** — network scanning and service detection

No additional Python packages are required. The script uses Python's built-in `subprocess` and `sys` modules.

## 📥 Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

Replace the URL with your repository's actual URL.

### 2. Verify the dependencies

```bash
python3 --version
naabu -version
nmap --version
```

Install Naabu and Nmap using their official installation instructions if they are not already available.

## ▶️ Usage

Run the script by providing a target IP address or hostname:

```bash
python3 scanner.py <target>
```

Example using an authorized test target:

```bash
python3 scanner.py 192.0.2.10
```

Replace the example address with a target you own or have explicit permission to scan.

## 📋 Example Workflow

Suppose Naabu discovers ports `22`, `80`, and `443`.

The script constructs the following Nmap command:

```bash
nmap -sV -sS -p 22,80,443 <target>
```

Nmap then attempts to identify the services and their versions on those ports.

**Options used:**

| Option | Purpose |
|---|---|
| `-host` | Specifies the target for Naabu |
| `-silent` | Reduces Naabu's output to discovered results |
| `-sV` | Enables service and version detection in Nmap |
| `-sS` | Uses TCP SYN scanning; typically requires elevated privileges |
| `-p` | Specifies the ports to scan |

## ⚠️ Limitations

- The script assumes Naabu's output contains ports in the expected `IP:PORT` format.
- If no ports are discovered, the script exits without running Nmap.
- Nmap's SYN scan may require administrator or root privileges.
- The script currently has basic error handling and does not explicitly check the exit status of either scanning tool.
- Only ports discovered by Naabu are passed to Nmap, so missed ports will not be examined in the second stage.

## 🔐 Responsible Use

This tool is intended for **learning, authorized security testing, and network reconnaissance**.

- Scan only systems you own or have explicit permission to test.
- Follow the applicable laws and the target organization's security policies.
- Avoid scanning public or third-party systems without authorization.

## 🎯 Learning Objectives

This project helped me explore:

- Automating command-line security tools with Python.
- Using `subprocess.run()` to execute external programs.
- Passing command-line arguments to Python scripts.
- Parsing tool output and chaining results between security tools.
- Understanding basic port discovery and service enumeration workflows.

## 🔮 Future Improvements

- Add validation for target input and command-line arguments.
- Improve subprocess error handling and exit-code checks.
- Add support for saving results to a file.
- Support configurable Naabu and Nmap options.
- Add structured logging and execution summaries.
- Improve port parsing and handle unexpected tool output safely.

## 📄 License

This project is open source. Consider adding a [MIT License](https://opensource.org/license/mit) if you want others to reuse and modify the code under its terms.
