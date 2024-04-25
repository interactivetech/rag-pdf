
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

`pachctl create repo code`

Add doc

`pachctl put file code@master: -f parsing/parsing.py`

`pachctl put file code@master: -f parsing/rag_schema.py`

`pachctl put file code@master: -f finetune/generate_qna_pairs.py`

`pachctl put file documents@master: -f output.pdf`

`pachctl put file documents@master: -f antonio-neri.xml`

parsing pipeline

`pachctl create pipeline -f pipelines/parsing.pipeline.json`

chunking pipeline

`pachctl create pipeline -f pipelines/chunking.pipeline.json`

embedding pipeline

`pachctl create pipeline -f pipelines/embedding.pipeline.json`




qna pipeline

`pachctl create pipeline -f pipelines/qna.pipeline.json`

finetune pipeline

`pachctl create pipeline -f pipelines/finetune.pipeline.json`

gui pipeline

`pachctl create pipeline -f pipelines/gui.pipeline.json`