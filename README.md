# Quaternion Encryption Tool (QET)

## Overview

**QET (Quaternion Encryption Tool)** is a command-line and web service application that provides encryption and decryption capabilities using quaternion mathematics. Quaternions, an extension of complex numbers, offer a unique and powerful method of securing messages and files. QET supports key management, multiple output formats, optional quaternion visualization, and a service mode that exposes FastAPI endpoints for performing oracle operations.

## Features

- **Encryption and Decryption**: Secure your messages and files using quaternion-based encryption.
- **Key Management**: Generate, save, load, and delete encryption keys, each identified by a unique GUID.
- **Multiple Output Formats**: Output encrypted and decrypted data in standard output, JSON files, or binary files.
- **Optional Visualization**: Plot quaternions used during encryption and decryption.
- **Support for Text and Binary Data**: Encrypt and decrypt both text messages and binary files.
- **Service Mode**: Run a FastAPI server to expose encryption and decryption operations as web services.

## Installation

### Download the Binary

1. **Visit the Releases Page**:
   - Go to the [QET releases page](https://github.com/blakdayz/qet/releases) and download the appropriate binary for your operating system.
   - Only M Series Apple Devices are currently supportedc 

### Linux / macOS

1. **Move the Binary to a Directory in Your PATH**:
   - After downloading the binary, move it to a directory in your `PATH`, such as `/usr/local/bin/`.

   ```bash
   sudo mv qet /usr/local/bin/
   sudo chmod +x /usr/local/bin/qet
   ```

2. **Verify the Installation**:
   - Run the following command to ensure QET is installed and accessible:

   ```bash
   qet --help
   ```

### Windows

1. **Download the QET Executable**:
   - Download `qet.exe` from the [QET releases page](https://github.com/yourusername/qet/releases).

2. **Move the Executable to a Directory in Your PATH**:
   - Alternatively, you can run it directly from the download location.

3. **Verify the Installation**:
   - Open Command Prompt and run:

   ```cmd
   qet --help
   ```

## Usage

### General Command Structure

```bash
qet <mode> <input> [options]
```

### Command Modes

#### 1. **Encrypt a Message or File**

- **Encrypt a text message and save the output to a JSON file:**
  ```bash
  qet encrypt "Your message here" --key mykey.json --output json
  ```

- **Encrypt a file and save the encrypted output in binary format:**
  ```bash
  qet encrypt myfile.txt --key mykey.json --file --output binary
  ```

- **Encrypt a message and output the encrypted quaternions to the console:**
  ```bash
  qet encrypt "Secret Message" --key mykey.json --output stdout
  ```

- **Encrypt a message with quaternion visualization:**
  ```bash
  qet encrypt "Message with plot" --key mykey.json --plot
  ```

#### 2. **Decrypt a Message or File**

- **Decrypt a JSON file containing quaternions and print the message:**
  ```bash
  qet decrypt output.json --key mykey.json --output stdout
  ```

- **Decrypt a binary file and save the decrypted data to a file:**
  ```bash
  qet decrypt output.bin --key mykey.json --binary --file
  ```

- **Decrypt and plot the quaternions:**
  ```bash
  qet decrypt output.json --key mykey.json --plot
  ```

#### 3. **Key Management**

- **Generate a new quaternion key with a GUID and save it to a file:**
  ```bash
  qet generate-key --key mykey.json
  ```

- **Delete an existing quaternion key file:**
  ```bash
  qet delete-key --key mykey.json
  ```

#### 4. **Service Mode**

Start a FastAPI server to perform oracle operations on quaternions via HTTP requests.

- **Run the FastAPI server:**
  ```bash
  qet service --host 127.0.0.1 --port 8000
  ```

- **Perform an oracle operation via HTTP POST:**

  Send a request to the `/oracle/` endpoint with a key and a list of quaternions to perform decryption or another operation.

  Example using `curl`:
  ```bash
  curl -X POST "http://127.0.0.1:8000/oracle/" -H "Content-Type: application/json" -d '{"key": "<your_key_json>", "quaternions": [{"w": 1.0, "x": 2.0, "y": 3.0, "z": 4.0}, {"w": 5.0, "x": 6.0, "y": 7.0, "z": 8.0}]}'
  ```

### Options

- **`--key <key_path>`**: Specify the path to the key file. The default is `key_quaternion.json`.
- **`--output <output_format>`**: Choose the output format: `stdout`, `json`, or `binary`.
- **`--file`**: Indicate that the input is a file rather than a direct message.
- **`--plot`**: Plot the quaternions used in encryption or decryption.
- **`--binary`**: Use binary format for input or output files.
- **`--host <host>`**: Specify the host for the FastAPI server in service mode.
- **`--port <port>`**: Specify the port for the FastAPI server in service mode.

## Examples

### 1. Encrypt a Message and Save to JSON

```bash
qet encrypt "Hello, World!" --key mykey.json --output json
```

### 2. Decrypt a JSON File and Print the Message

```bash
qet decrypt output.json --key mykey.json
```

### 3. Encrypt a File and Output the Result in Binary

```bash
qet encrypt myfile.txt --key mykey.json --file --output binary
```

### 4. Generate a New Encryption Key

```bash
qet generate-key --key mykey.json
```

### 5. Delete an Encryption Key

```bash
qet delete-key --key mykey.json
```

### 6. Start the FastAPI Service

```bash
qet service --host 127.0.0.1 --port 8000
```

### 7. Perform Oracle Operations via the FastAPI Service

```bash
curl -X POST "http://127.0.0.1:8000/oracle/" -H "Content-Type: application/json" -d '{"key": "<your_key_json>", "quaternions": [{"w": 1.0, "x": 2.0, "y": 3.0, "z": 4.0}, {"w": 5.0, "x": 6.0, "y": 7.0, "z": 8.0}]}'
```

## Contributing

Contributions are welcome! If you would like to contribute, please fork this repository, make your changes, and submit a pull request.

## License

This project is not licensed for commercial use, is offereed AS IS with NO warranty implied. All rights reserved to the author Derek Hinch <derek.hinch@qompute.ai>
