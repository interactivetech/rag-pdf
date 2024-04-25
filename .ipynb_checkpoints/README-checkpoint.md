
# Connect to deployed pachyderm application
`pachctl connect pachd-peer.pachyderm.svc.cluster.local:30653`
# list current projects
`pachctl list project`

`pachctl version`

# Create Pachyderm application
`pachctl create project pdf-rag-andrew`
# Set pachctl's active context to the deploy-rag project
`pachctl config update context --project pdf-rag-andrew`


repo

`pachctl create repo documents`