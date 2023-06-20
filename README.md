Issue with Prisma generating migration.

# Setup
1. npm install
1. docker compose -f docker-compose.yml up -d --wait 
1. sleep 3
1. npx prisma migrate dev

## Error
```
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
Datasource "db": PostgreSQL database "app", schema "public" at "localhost:26257"

Error: db error: ERROR: internal error: executing declarative schema change StatementPhase stage 1 of 1 with 98 MutationType ops (rollback=false) for DROP DATABASE: error executing StatementPhase stage 1 of 1 with 98 MutationType ops: relation "Post" (111): origin table "ReadPosts" (112) is dropped
DETAIL: • Schema change plan for DROP DATABASE IF EXISTS ‹"prisma_migrate_shadow_db_c213f6a1-a0e5-4663-8fe1-fea779b4c712"›;
│
├── • StatementPhase
│   │
│   └── • Stage 1 of 1 in StatementPhase
...
(lines truncated)
...
stack trace:
github.com/cockroachdb/cockroach/pkg/sql/catalog/tabledesc/validate.go:510: validateInboundFK()
github.com/cockroachdb/cockroach/pkg/sql/catalog/tabledesc/validate.go:244: ValidateBackReferences()
github.com/cockroachdb/cockroach/pkg/sql/catalog/internal/validate/validate.go:110: func3()
github.com/cockroachdb/cockroach/pkg/sql/catalog/internal/validate/validate.go:198: validateDescriptorsAtLevel()
github.com/cockroachdb/cockroach/pkg/sql/catalog/internal/validate/validate.go:105: Validate()
github.com/cockroachdb/cockroach/pkg/sql/catalog/descs/validate.go:40: Validate()
github.com/cockroachdb/cockroach/pkg/sql/catalog/descs/validate.go:74: ValidateUncommittedDescriptors()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scdeps/exec_deps.go:206: Validate()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scexec/exec_immediate_mutation.go:146: exec()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scexec/exec_mutation.go:37: executeMutationOps()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scexec/executor.go:28: ExecuteStage()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scrun/scrun.go:188: executeStage()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scrun/scrun.go:103: runTransactionPhase()
github.com/cockroachdb/cockroach/pkg/sql/schemachanger/scrun/scrun.go:54: RunStatementPhase()
github.com/cockroachdb/cockroach/pkg/sql/schema_change_plan_node.go:279: startExec()
github.com/cockroachdb/cockroach/pkg/sql/plan.go:519: func2()
github.com/cockroachdb/cockroach/pkg/sql/walk.go:112: func1()
github.com/cockroachdb/cockroach/pkg/sql/walk.go:299: visitInternal()
github.com/cockroachdb/cockroach/pkg/sql/walk.go:79: visit()
github.com/cockroachdb/cockroach/pkg/sql/walk.go:43: walkPlan()
github.com/cockroachdb/cockroach/pkg/sql/plan.go:522: startExec()
github.com/cockroachdb/cockroach/pkg/sql/plan_node_to_row_source.go:174: Start()
github.com/cockroachdb/cockroach/pkg/sql/colexec/columnarizer.go:183: Init()
github.com/cockroachdb/cockroach/pkg/sql/colflow/stats.go:94: init()
github.com/cockroachdb/cockroach/pkg/sql/colexecerror/error.go:92: CatchVectorizedRuntimeError()
github.com/cockroachdb/cockroach/pkg/sql/colflow/stats.go:103: Init()
github.com/cockroachdb/cockroach/pkg/sql/colflow/flow_coordinator.go:245: func1()
github.com/cockroachdb/cockroach/pkg/sql/colexecerror/error.go:92: CatchVectorizedRuntimeError()
github.com/cockroachdb/cockroach/pkg/sql/colflow/flow_coordinator.go:244: init()
github.com/cockroachdb/cockroach/pkg/sql/colflow/flow_coordinator.go:278: Run()
github.com/cockroachdb/cockroach/pkg/sql/colflow/vectorized_flow.go:325: Run()
github.com/cockroachdb/cockroach/pkg/sql/distsql_running.go:902: Run()

HINT: You have encountered an unexpected error.

Please check the public issue tracker to check whether this problem is
already tracked. If you cannot find it there, please report the error
with details by creating a new issue.

If you would rather not post publicly, please contact us directly
using the support form.

We appreciate your feedback.

   0: sql_migration_connector::validate_migrations
           with namespaces=None
             at migration-engine/connectors/sql-migration-connector/src/lib.rs:304
   1: migration_core::state::DevDiagnostic
             at migration-engine/core/src/state.rs:269
```