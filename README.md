# denv

`denv` (Docker environment) is used to manage Docker containers in Wazo integration tests to ease development workflow.

Example:

```
(webhookd-test)user ~/data/git/webhookd/integration_tests $ denv enter calld base
Removing calld_sync_run_1         ... done
Removing calld_webhookd_1         ... done
Removing calld_third-party-http_1 ... done
Removing calld_postgres_1         ... done
Removing calld_rabbitmq_1         ... done
Removing calld_auth_1             ... done
Creating calld_rabbitmq_1 ...
Creating calld_auth_1 ...
Creating calld_third-party-http_1 ...
Creating calld_postgres_1 ...
Creating calld_rabbitmq_1
Creating calld_auth_1
Creating calld_postgres_1
Creating calld_third-party-http_1 ... done
Creating calld_webhookd_1 ...
Creating calld_webhookd_1 ... done
172.17.0.3:1080 up!
172.17.0.4:5432 up!
...172.17.0.5:5672 up!
172.17.0.6:9300 up!
172.17.0.2:9497 up!

[base](webhookd-test)seb ~/data/git/webhookd/integration_tests $ denv restart webhookd
Restarting calld_webhookd_1 ... done

[base](webhookd-test)seb ~/data/git/webhookd/integration_tests $ denv exit
Killing calld_webhookd_1         ... done
Killing calld_third-party-http_1 ... done
Killing calld_postgres_1         ... done
Killing calld_rabbitmq_1         ... done
Killing calld_auth_1             ... done

(webhookd-test)seb ~/data/git/webhookd/integration_tests $
```

When entering a denv, the containers of the given asset are started. This allows a developer to run tests quicker when writing them, according to the following workflow:

```
denv enter ...
*run the test*... FAIL
*edit the test*
*run the test*... FAIL
*edit the source code under test*
*restart the daemon* (denv restart)
*run the test*... PASS
denv exit
```

This avoids the starting and stopping of every container when running a few integration tests that need the same asset.

`denv` disables the starting/stopping of the containers via the `TEST_DOCKER=ignore` environment variable.

## Installing

```
git clone https://github.com/wazo-platform/denv

# bash
echo "source $PWD/denv/denv" >> ~/.bashrc

# zsh
echo "source $PWD/denv/denv" >> ~/.zshrc
```

## Tips

`denv enter` is aliased to `denv e`.
`denv restart` is aliased to `denv r`.
`denv exit` is aliased to `denv x`.
`denv pull` is aliased to `denv p`.
`denv logs` is aliased to `denv log` and `denv l`.
`denv traceback` is aliased to `denv tb` and `denv t`.
