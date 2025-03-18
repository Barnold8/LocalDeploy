# Idea:

## High-Level Workflow

### Repository Monitoring
- Use a tool or script to watch for changes in your repository (e.g., using Git hooks like `pre-push` or `post-commit`).

### Dockerized Language Environments
- Create Docker images tailored to each language or project. Each image would:
  - Install the language runtime (e.g., Python, Node.js, Go).
  - Set up project-specific dependencies (e.g., `requirements.txt`, `package.json`, `go.mod`).
- Use `docker-compose` for managing multiple containers if needed.

### Host-Container Communication
- Implement a mechanism to send the results back to the host:
  - Use a **shared volume** to write logs and a status file (e.g., `status.txt` containing `0` or `1`).
  - Use an **exit code** from the container process, which can be read by the host script.

### Test Execution
- Inside the container:
  - Run tests using the relevant test frameworks (e.g., `pytest`, `go test`, `jest`).
  - Write detailed logs to a shared volume accessible by the host.

### Host Program
- A lightweight script or program on the host (e.g., Python or Bash) could:
  - Trigger Docker container runs.
  - Monitor the status file or capture the container's exit code.
  - Collect logs and provide notifications or updates.

### Log Aggregation and Reporting
- Store logs in a structured format (e.g., JSON or plain text).
- Use a web interface or a CLI tool to view logs and test results.

