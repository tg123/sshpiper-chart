# Helm Chart for sshpiper

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/sshpiper)](https://artifacthub.io/packages/helm/sshpiper/sshpiper)


<https://github.com/tg123/sshpiper>


## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

  helm repo add sshpiper https://tg123.github.io/sshpiper-chart

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
sshpiper` to see the charts.

To install the sshpiper chart:

    helm install my-sshpiper sshpiper/sshpiper

To uninstall the chart:

    helm delete my-sshpiper
