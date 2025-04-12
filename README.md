## Script: Analyze Sessions Holding Database Locks with Kill Option

**Description**:
This script retrieves detailed information about all active sessions that currently hold **granted locks** on databases. It shows session I/O metrics, user and network info, currently executing SQL, and includes a generated `KILL` command for session termination.

**Features**:
- Optional filtering by database name (`@dbname`)
- Shows SQL query being executed using `sys.dm_exec_sql_text`
- Includes read/write activity and session metadata
- Tracks client IP and hostname
- Generates `KILL` command string for troubleshooting

**Columns**:
- `session_id`, `login_name`, `program_name`, `host_name`
- `reads`, `writes`, `logical_reads`
- `Query`: The currently running SQL
- `KillCommand`: Command string to end the session

**Use Case**:
- Monitor which sessions are holding critical database-level locks
- Identify long-running or blocking sessions
- Generate `KILL` commands for manual intervention (use with care)

**Requirements**:
- SQL Server 2005 or later
- `VIEW SERVER STATE` permission

**Notes**:
- `@dbname` can be set to a specific database or left NULL for all
- Use caution when executing generated `KILL` commands — always validate first
- This script only shows **GRANTED locks** (`request_status = 'GRANT'`)
