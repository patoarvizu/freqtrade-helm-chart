# freqtrade-helm-chart

A Helm chart for deploying [freqtrade](https://github.com/freqtrade/freqtrade).

**DO NOT USE THIS CHART FOR LIVE TRADING IF YOU'RE NOT SURE WHAT YOU'RE DOING.** This is still a work in progress with rough edges that might cost you real money. For now, the main purpose of this chart is to get familiar with how freqtrade works.

Also, as with anything crypto, make sure you do your due dilligence and only risk what you can afford to lose.

## Chart

The [`chart`](./chart) directory contains the Helm 3 chart for deploying a freqtrade bot and/or running backtests. Support for running hyperopt is planned for later. This chart isn't published anywhere yet, but it will eventually be published on GitHub Pages.

## Testing locally

If you don't have a full-fledged Kubernetes environment and want to test things locally and see them in action, follow the instructions under the [`test-local`](./test-local) directory. 
