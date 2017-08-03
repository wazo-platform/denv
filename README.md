# denv

`denv` is used to manage Docker containers in Wazo integration tests to ease development workflow.

Example:

```
(webhookd-test)user ~/data/git/webhookd/integration_tests $ denv enter base
Removing base_sync_run_1         ... done
Removing base_webhookd_1         ... done
Removing base_third-party-http_1 ... done
Removing base_postgres_1         ... done
Removing base_rabbitmq_1         ... done
Removing base_auth_1             ... done
Creating base_rabbitmq_1 ...
Creating base_auth_1 ...
Creating base_third-party-http_1 ...
Creating base_postgres_1 ...
Creating base_rabbitmq_1
Creating base_auth_1
Creating base_postgres_1
Creating base_third-party-http_1 ... done
Creating base_webhookd_1 ...
Creating base_webhookd_1 ... done
172.17.0.3:1080 up!
172.17.0.4:5432 up!
...172.17.0.5:5672 up!
172.17.0.6:9300 up!
172.17.0.2:9497 up!

[base](webhookd-test)seb ~/data/git/webhookd/integration_tests $ denv restart webhookd
Restarting base_webhookd_1 ... done

[base](webhookd-test)seb ~/data/git/webhookd/integration_tests $ denv exit
Killing base_webhookd_1         ... done
Killing base_third-party-http_1 ... done
Killing base_postgres_1         ... done
Killing base_rabbitmq_1         ... done
Killing base_auth_1             ... done

(webhookd-test)seb ~/data/git/webhookd/integration_tests $
```

When entering a denv, the containers of the given asset are started. This allows a developer to run tests quicker when writing them, according to the following workflow:

```
denv enter
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
git clone https://github.com/wazo-pbx/denv

# bash
echo "source $PWD/denv/denv" >> ~/.bashrc

# zsh
mkdir -p ~/.zsh
ln -s "$PWD/denv/denv" ~/.zsh
```

## Tips

`denv enter` is aliased to `denv e`.
`denv restart` is aliased to `denv r`.
`denv exit` is aliased to `denv x`.
