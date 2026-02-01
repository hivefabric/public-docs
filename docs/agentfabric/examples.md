# AgentFabric Examples

## Basic Sequential Workflow

A simple data pipeline:

```yaml
version: "1.0"
name: "data-pipeline"

nodes:
  - id: "extract"
    type: "step"
    action: "extract_from_db"
    params:
      query: "SELECT * FROM users"
  
  - id: "transform"
    type: "step"
    action: "transform_data"
    depends_on: ["extract"]
    params:
      format: "json"
  
  - id: "load"
    type: "step"
    action: "load_to_warehouse"
    depends_on: ["transform"]
```

## Fork-Join Pattern

Process data in parallel, then aggregate:

```yaml
version: "1.0"
name: "parallel-processing"

nodes:
  - id: "split-data"
    type: "step"
    action: "split_dataset"
  
  - id: "process-chunks"
    type: "fork"
    join_strategy: "all"
    children:
      - id: "chunk-1"
        type: "step"
        action: "process_chunk"
        params: {index: 0}
      - id: "chunk-2"
        type: "step"
        action: "process_chunk"
        params: {index: 1}
      - id: "chunk-3"
        type: "step"
        action: "process_chunk"
        params: {index: 2}
  
  - id: "merge-results"
    type: "step"
    action: "merge"
    depends_on: ["process-chunks"]
```

## Human-in-the-Loop

Include manual approval steps:

```yaml
version: "1.0"
name: "approval-workflow"

nodes:
  - id: "generate-report"
    type: "step"
    action: "generate_report"
  
  - id: "review"
    type: "step"
    action: "wait_for_approval"
    params:
      timeout: 86400
  
  - id: "publish"
    type: "step"
    action: "publish_report"
    depends_on: ["review"]
```

## Error Handling

```yaml
version: "1.0"
name: "resilient-pipeline"

nodes:
  - id: "fetch"
    type: "step"
    action: "fetch_with_retry"
    params:
      max_retries: 3
      backoff: "exponential"
  
  - id: "fallback"
    type: "step"
    action: "use_cache"
    on_failure: "fetch"
```
