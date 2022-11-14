# inlets troubleshooting

[inlets.dev](https://inlets.dev) troubleshooting.

So far, I've had some issues getting to work out of the box. I think this
mostly comes down to the documentation drifting out of sync with the project.

```shell
inletsctl create \
--access-token-file ~/.doctl-token \
--provider digitalocean \
--region sgp1 \
--letsencrypt-domain inlets.cupscanteen.com \
--letsencrypt-domain t.cupscanteen.com \
--letsencrypt-domain slack.cupscanteen.com \
--letsencrypt-email webmaster@cupscanteen.com
```

Sometimes this doesn't work. So to get it working, I jump on the host. For
DO the password is emailed when you create the host (which the above step
does for you).

```shell
vim /etc/default/inlets-pro
# add any extra domains with --letsencrypt-domain <sub>.<domain>.<tld>
# after the DOMAINS=
```

The documentation states its `--letsencrypt-domain=foo.com,bar.com` but
this does not seem to work.

`systemctl restart inlets-pro` and see if the process has started correctly. It
can take time to get the cert from Let's Encrypt.

Tags:

    #inlets #tunnelling #troubleshooting
