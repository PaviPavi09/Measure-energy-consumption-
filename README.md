import subprocess

# Define the command to run powerstat
command = "powerstat -d 1"

# Execute the command and capture its output
process = subprocess.Popen(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)

# Collect and print the output
while True:
    output = process.stdout.readline().decode('utf-8')
    if output == '' and process.poll() is not None:
        break
    if output:
        print(output.strip())

# Wait for the process to complete
process.wait()

# Check for errors
if process.returncode != 0:
    print(f"Error: {process.stderr.read().decode('utf-8')}")# Measure-energy-consumption-
