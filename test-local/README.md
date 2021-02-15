# Running the chart locally

## Notes

- The defaults under the `./values/` directory will be very trivial. **DO NOT USE THEM FOR LIVE TRADING**.
- If the chart options aren't documented yet, you can look at the [default values](../chart/values.yaml) on the chart, and most of them should be self-explanatory if you're already familiar with freqtrade.

## Prerequisites

- [Helm 3](https://helm.sh/docs/intro/install/).
- [helmfile](https://github.com/roboll/helmfile).
- [Docker](https://docs.docker.com/get-docker/).
- [k3d](https://k3d.io/#installation).
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

## Secrets

If you're setting secret values such as your exchange's API token, your Telegram token, the API server's credentials, etc., you'll need to add them to add a file under `./values/` called `secrets.yaml` with the contents below (but filling in your own secrets as necessary). **AGAIN, DON'T USE THIS FOR LIVE TRADING IF YOU DON'T KNOW WHAT YOU'RE DOING.**

```
config:
  exchange:
    key: yourkey
    secret: yoursecret
  telegram:
    token: yourtoken
    chat_id: yourid
  api_server:
    username: yourusername
    password: yoursecret
    jwt_secret_key: yourjwtkey
```

## Steps

- Run `export KUBECONFIG=~/.k3d/k3s-default-config`. (This is done to avoid overwriting any local Kubernetes configuration files you may have.)
- Run `make cluster`.
- Run `make sync`.
- Run `kubectl -n freqtrade get pods` and wait for all pods to either be in `Running` or `Completed`.
- This will launch one backtesting simulation, with some sane defaults and the `SampleStrategy`.
- Go to `http://localhost:8080/login` and you should be able to log in to the FreqUI. The API is also available at `http://localhost:8080/api/v1`.
- To see the results of the backtesting, go to `http://localhost:8080/results`.
- Run `make sync` again. This will trigger another backtest. After it's finished, you can see the updated results at `http://localhost:8080/results`.