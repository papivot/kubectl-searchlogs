# kubectl-searchlogs

A `kubectl` plugin to grep logs across all pods in a namespace, sorted by time. This tool is helpful for debugging issues spanning multiple pods or services, allowing you to view a chronological timeline of events matching a search term.

## Features

- **Search across all pods**: Greps logs from every pod in the specified namespace.
- **Unified Timeline**: Merges and sorts logs from all pods by timestamp.
- **Smart Defaults**:
  - Automatically detects the current namespace if not provided.
  - Defaults to searching the last 30 minutes.

## Installation

1. Download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/your-repo/kubectl-searchlogs/main/kubectl-searchlogs
   ```
2. Make it executable:
   ```bash
   chmod +x kubectl-searchlogs
   ```
3. Move it to a directory in your `PATH` (e.g., `/usr/local/bin`):
   ```bash
   sudo mv kubectl-searchlogs /usr/local/bin/kubectl-searchlogs
   ```

## Usage

```bash
kubectl searchlogs [-n <NAMESPACE>] [-t <TIME_WINDOW>] <SEARCH_STRING>
```

### Options

| Option | Description | Default |
|--------|-------------|---------|
| `-n` | Target namespace | Current context namespace or `default` |
| `-t` | Time window (e.g., `30s`, `5m`, `1h`) | `30m` |
| `-h` | Show help message | - |

### Examples

**Search for "Error" in the current namespace (last 30m):**
```bash
kubectl searchlogs "Error"
```

**Search for "Transaction Failed" in the `payment-service` namespace (last 1 hour):**
```bash
kubectl searchlogs -n payment-service -t 1h "Transaction Failed"
```

**Search for "Exception" in the last 10 minutes:**
```bash
kubectl searchlogs -t 10m "Exception"
```

## Requirements

- `kubectl` must be installed and configured.
- `bash`, `grep`, `sed`, `sort`, `xargs`.
