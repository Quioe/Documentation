@9Aryan-kushwaha ➜ /workspaces/Quie (main) $ docker-compose logs
qkd-sim-1  | /app/main.py:156: DeprecationWarning: 
qkd-sim-1  |         on_event is deprecated, use lifespan event handlers instead.
qkd-sim-1  | 
qkd-sim-1  |         Read more about it in the
qkd-sim-1  |         [FastAPI docs for Lifespan Events](https://fastapi.tiangolo.com/advanced/events/).
qkd-sim-1  |         
qkd-sim-1  |   @app.on_event("startup")
qkd-sim-1  | INFO:     Started server process [1]
qkd-sim-1  | INFO:     Waiting for application startup.
qkd-sim-1  | INFO:     Application startup complete.
qkd-sim-1  | INFO:     Uvicorn running on http://0.0.0.0:8001 (Press CTRL+C to quit)
redis-1    | 1:C 22 Sep 2025 09:35:51.973 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
redis-1    | 1:C 22 Sep 2025 09:35:51.973 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis-1    | 1:C 22 Sep 2025 09:35:51.973 * Redis version=7.4.5, bits=64, commit=00000000, modified=0, pid=1, just started
redis-1    | 1:C 22 Sep 2025 09:35:51.973 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
redis-1    | 1:M 22 Sep 2025 09:35:51.974 * Increased maximum number of open files to 10032 (it was originally set to 1024).
redis-1    | 1:M 22 Sep 2025 09:35:51.974 * monotonic clock: POSIX clock_gettime
redis-1    | 1:M 22 Sep 2025 09:35:51.975 * Running mode=standalone, port=6379.
redis-1    | 1:M 22 Sep 2025 09:35:51.975 * Server initialized
redis-1    | 1:M 22 Sep 2025 09:35:51.975 * Ready to accept connections tcp
redis-1    | 1:M 22 Sep 2025 10:35:52.001 * 1 changes in 3600 seconds. Saving...
redis-1    | 1:M 22 Sep 2025 10:35:52.001 * Background saving started by pid 20
redis-1    | 20:C 22 Sep 2025 10:35:52.005 * DB saved on disk
redis-1    | 20:C 22 Sep 2025 10:35:52.005 * Fork CoW for RDB: current 0 MB, peak 0 MB, average 0 MB
redis-1    | 1:M 22 Sep 2025 10:35:52.102 * Background saving terminated with success
redis-1    | 1:C 24 Sep 2025 08:48:16.645 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
redis-1    | 1:C 24 Sep 2025 08:48:16.646 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis-1    | 1:C 24 Sep 2025 08:48:16.646 * Redis version=7.4.5, bits=64, commit=00000000, modified=0, pid=1, just started
redis-1    | 1:C 24 Sep 2025 08:48:16.646 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
redis-1    | 1:M 24 Sep 2025 08:48:16.647 * Increased maximum number of open files to 10032 (it was originally set to 1024).
redis-1    | 1:M 24 Sep 2025 08:48:16.647 * monotonic clock: POSIX clock_gettime
redis-1    | 1:M 24 Sep 2025 08:48:16.648 * Running mode=standalone, port=6379.
redis-1    | 1:M 24 Sep 2025 08:48:16.648 * Server initialized
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * Loading RDB produced by version 7.4.5
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * RDB age 166344 seconds
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * RDB memory usage when created 1.05 Mb
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * Done loading RDB, keys loaded: 1, keys expired: 0.
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * DB loaded from disk: 0.002 seconds
redis-1    | 1:M 24 Sep 2025 08:48:16.651 * Ready to accept connections tcp
kms-1      | 2025-09-24 08:48:19,915 - __main__ - INFO - Successfully connected to Redis
mailhog-1  | 2025/09/22 09:35:52 Using in-memory storage
mailhog-1  | 2025/09/22 09:35:52 [SMTP] Binding to address: 0.0.0.0:1025
mailhog-1  | [HTTP] Binding to address: 0.0.0.0:8025
mailhog-1  | 2025/09/22 09:35:52 Serving under http://0.0.0.0:8025/
mailhog-1  | Creating API v1 with WebPath: 
mailhog-1  | Creating API v2 with WebPath: 
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
gateway-1  | Traceback (most recent call last):
gateway-1  |   File "/app/main.py", line 21, in <module>
gateway-1  |     import aiohttp
gateway-1  | ModuleNotFoundError: No module named 'aiohttp'
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | [APIv1] KEEPALIVE /api/v1/events
mailhog-1  | 2025/09/24 08:48:15 Using in-memory storage
mailhog-1  | 2025/09/24 08:48:15 [SMTP] Binding to address: 0.0.0.0:1025
mailhog-1  | 2025/09/24 08:48:15 Serving under http://0.0.0.0:8025/
mailhog-1  | [HTTP] Binding to address: 0.0.0.0:8025
mailhog-1  | Creating API v1 with WebPath: 
mailhog-1  | Creating API v2 with WebPath: 
@9Aryan-kushwaha ➜ /workspaces/Quie (main) $ 