
# Connect to deployed pachyderm application
`pachctl connect pachd-peer.pachyderm.svc.cluster.local:30653`
# list current projects
`pachctl list project`

`pachctl version`

# Create Pachyderm application
`pachctl create project pdf-rag-andrew`
# Set pachctl's active context to the deploy-rag project
`pachctl config update context --project pdf-rag-andrew`

## Pipeline will be available at the url:
``

repo

`pachctl create repo documents`

`pachctl create repo code`

Add doc

`pachctl put file code@master: -f parsing/parsing.py`

`pachctl put file code@master: -f parsing/rag_schema.py`

`pachctl put file code@master: -f finetune/generate_qna_pairs.py`

`pachctl put file code@master: -f embedding/embed.py`

`pachctl put file documents@master: -f output.pdf`

`pachctl put file documents@master: -f antonio-neri.xml`
`pachctl put file documents@master: -f aruba_wifi_7_press.xml`
`pachctl put file documents@master: -f e2e_ai_platform_press_release.xml`

parsing pipeline

`pachctl create pipeline -f pipelines/parsing.pipeline.json`

chunking pipeline

`pachctl create pipeline -f pipelines/chunking.pipeline.json`

embedding pipeline

`pachctl create pipeline -f pipelines/embedding.pipeline.json`




qna pipeline

`pachctl create pipeline -f pipelines/qna.pipeline.json`


`pachctl create pipeline -f pipelines/finetune.pipeline.json`

gui pipeline

`pachctl create pipeline -f pipelines/gui.pipeline.json`

To access GUI:

Note: There is an issue with the houston cluster where there are not enough IP addresses for service pipeline.

Run:

`ssh andrew@mlds-mgmt.us.rdlabs.hpecorp.net -L 8080:localhost:8080`

Run command:

`kubectl port-forward -n pachyderm svc/pdf-rag-andrew-gui-v1-user 8080:80`

Open web browswer and go to url:

`localhost:8080`

Ask in the UI:

`Who is Antonio Neri?`


Now ask, the app wont answer it correctly:
`Who is Neil MacDonald?`

We will show the key value proposition with a data driven pipeline, add more documents, the RAG app will automatically be updated. 

In the terminal, add new document:

`pachctl put file documents@master: -f neil-macdonald.xml`

When pipeline is done, refresh webpage and ask:
`Who is Neil MacDonald?`

Delete pipelines

`pachctl delete pipeline gui`
`pachctl delete pipeline finetune-embedding`
`pachctl delete pipeline generate-qna`
`pachctl delete pipeline embed-docs`
`pachctl delete pipeline chunk-doc`
`pachctl delete pipeline parse-docs`

```
pachctl create repo documents
pachctl create repo code

pachctl put file documents@master: -f antonio-neri.xml
pachctl put file code@master: -f parsing/parsing.py
pachctl put file code@master: -f finetune/generate_qna_pairs.py
pachctl put file code@master: -f embedding/embed.py

pachctl create pipeline -f pipelines/parsing.pipeline.json
pachctl create pipeline -f pipelines/chunking.pipeline.json
pachctl create pipeline -f pipelines/embedding.pipeline.json
pachctl create pipeline -f pipelines/qna.pipeline.json
pachctl create pipeline -f pipelines/gui.pipeline.json
```

SSH TO MLDS MGMT node


Run command 
`kubectl port-forward -n pachyderm svc/pdf-rag-andrew-gui-v1-user 8080:80`

`go to localhost:8080`

`ask question:  Who is Antonio Neri?`

Then ask

`Who is Neil MacDonald?`



Run command

`pachctl put file documents@master: -f neil-macdonald.xml`

Run 

(4/26/2028) MLDM has a bug right now in service pipelines. you have to kill the pipeline to get the new data

`pachctl delete pipeline gui`

`pachctl create pipeline -f pipelines/gui.pipeline.json`

`Select clear cache`

reload webpage , and then ask

`Who is Neil MacDonald?`


```
pachctl delete pipeline gui
pachctl delete pipeline generate-qna
pachctl delete pipeline embed-docs
pachctl delete pipeline chunk-doc
pachctl delete pipeline parse-docs
pachctl delete repo documents
pachctl delete repo code
```