
## Deployment to Servers or Public Cloud

The following guides can help with the deployment to public cloud providers:
* [AWS](aws.md)
* [DigitalOcean](digital-ocean.md)
* [Heroku](heroku.md)
* [Kubernetes & Docker](packaging.md#docker)
* [GCP](gcp.md)
* _Have a guides for other popular public clouds like Azure? Add it here!_

If you are deploying to you own servers (e.g. bare metal, VMs or Docker) there are several strategies for packaging Swift applications for deployment, see the [Packaging Guide](packaging.md) for more information.

### Deploying a Debuggable Configuration (Production on Linux)

- If you have `--privileged`/`--security-opt seccomp=unconfined` containers or are running in VMs or even bare metal, you can run your binary with

        lldb --batch -o "break set -n main --auto-continue 1 -C \"process handle SIGPIPE -s 0\"" -o run -k "image list" -k "register read" -k "bt all" -k "exit 134" ./my-program

    instead of `./my-program` to get something something akin to a 'crash report' on crash.

- If you don't have `--privileged` (or `--security-opt seccomp=unconfined`) containers (meaning you won't be able to use `lldb`) or you don't want to use lldb, consider using a library like [`swift-backtrace`](https://github.com/swift-server/swift-backtrace) to get stack traces on crash.
