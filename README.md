# mailcow exporter

[Prometheus](https://prometheus.io) exporter for information about a
[mailcow](https://github.com/mailcow/mailcow-dockerized) instance.

## Usage

In order to use the exporter, you will need to get a readonly API token
for the instance first. To extract that, log into the management interface
and create one under 'Access > API'.

```
$ docker run \
    -e 'MAILCOW_HOST=mail.mydomain.com' \
    -e 'MAILCOW_API_KEY=...' \
    -p '9099:9099' \
    thej6s/mailcow-exporter
```

## Example metrics

```
mailcow_mailbox_last_login{mailbox="foo@bar.com"} 1.599255303e+09
mailcow_mailbox_last_login{mailbox="test@bar.com"} 1.599247706e+09

mailcow_mailbox_messages{mailbox="foo@bar.com"} 23476
mailcow_mailbox_messages{mailbox="test@bar.com"} 1891

mailcow_mailbox_quota_allowed{mailbox="foo@bar.com"} 3.221225472e+09
mailcow_mailbox_quota_allowed{mailbox="test@bar.com"} 3.221225472e+09

mailcow_mailbox_quota_used{mailbox="foo@bar.com"} 1.919023167e+09
mailcow_mailbox_quota_used{mailbox="test@bar.com"} 1.844312552e+09

mailcow_mailq{queue="deferred",sender="foo@bar.com"} 2
mailcow_mailq{queue="deferred",sender="test@bar.com"} 1

# HELP mailcow_quarantine_age Age of quarantined items in seconds
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="10800"} 0
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="43200"} 0
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="86400"} 0
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="259200"} 3
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="604800"} 9
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="1.2096e+06"} 12
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="2.592e+06"} 41
mailcow_quarantine_age_bucket{recipient="foo@bar.com",le="+Inf"} 147
mailcow_quarantine_age_sum{recipient="foo@bar.com"} 1.301292926e+09
mailcow_quarantine_age_count{recipient="foo@bar.com"} 147
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="10800"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="43200"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="86400"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="259200"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="604800"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="1.2096e+06"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="2.592e+06"} 0
mailcow_quarantine_age_bucket{recipient="test@bar.com",le="+Inf"} 2
mailcow_quarantine_age_sum{recipient="test@bar.com"} 2.7138547e+07
mailcow_quarantine_age_count{recipient="test@bar.com"} 2

mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="0"} 0
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="10"} 0
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="20"} 41
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="40"} 122
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="60"} 136
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="80"} 141
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="100"} 141
mailcow_quarantine_score_bucket{recipient="foo@bar.com",le="+Inf"} 147
mailcow_quarantine_score_sum{recipient="foo@bar.com"} 16225.91000000001
mailcow_quarantine_score_count{recipient="foo@bar.com"} 147
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="0"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="10"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="20"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="40"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="60"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="80"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="100"} 0
mailcow_quarantine_score_bucket{recipient="test@bar.com",le="+Inf"} 2
mailcow_quarantine_score_sum{recipient="test@bar.com"} 3988.03
mailcow_quarantine_score_count{recipient="test@bar.com"} 2

mailcow_quarantine_count{is_virus="0",recipient="foo@bar.com"} 147
mailcow_quarantine_count{is_virus="0",recipient="test@bar.com"} 2
mailcow_quarantine_count{is_virus="1",recipient="foo@bar.com"} 0
mailcow_quarantine_count{is_virus="1",recipient="test@bar.com"} 0
```
