# CHANGELOG

## 6.8.2-1

* Removes previously added `INPUT_KUBERNETES_FILE_CHUNK_COUNT`, `INPUT_KUBERNETES_FILE_CHUNK_SIZE` environment variables 
  due to the version of `logstash-input-file` plugin used.
* Preinstalls `logstash-input-file` plugin v4.0.5 due to log change tracking issues in v.4.1.x.
* Renames `logstash.yml` config option:
	`xpack.monitoring.elasticsearch.url` -> `xpack.monitoring.elasticsearch.hosts`

## 6.8.1-3

* Removes `ELASTICSEARCH_FLUSH_SIZE` as it's now obsolete.

## 6.8.1-2

* Adds the following environment variables:
	* `INPUT_KUBERNETES_FILE_CHUNK_COUNT` - [file_chunk_count](https://www.elastic.co/guide/en/logstash/6.8/plugins-inputs-file.html#plugins-inputs-file-file_chunk_count). Default: 32.
	* `INPUT_KUBERNETES_FILE_CHUNK_SIZE` - [file_chunk_size](https://www.elastic.co/guide/en/logstash/6.8/plugins-inputs-file.html#plugins-inputs-file-file_chunk_size). Default: 32768 (32KB).

	By default Logstash will read at most 1MB chunks at a time from each Docker container log file.

## 6.8.1-1

* Upgrades base image to fedora:30
* Upgrades Logstash to version 6.8.1: https://www.elastic.co/guide/en/logstash/6.8/releasenotes.html
* Bumps `journald` plugin version
* Installs `statsd` plugin as no longer part of the standard install.
* The following environment variables are ADDED:
	* `LS_NODE_NAME`
	* `LS_HTTP_HOST`
* Options added to README:
	* `LS_JAVA_OPTS`

## 5.6.16-1

* Upgrades Logstash to version 5.6.16: https://www.elastic.co/guide/en/logstash/5.6/releasenotes.html

* Added options:
	* `LS_MONITORING_ENABLE` - Whether to enable Logstash xpack monitoring. Default: `false`
	* `ELASTICSEARCH_SCHEME` - Elasticsearch HTTP scheme. Default: `http`.

### Notes:

`ELASTICSEARCH_SCHEME` should be set to `https` where appropriate, but is only actually used when LS_MONITORING_ENABLE is `true`.

Elasticsearch outputs with `document_type` are deprecated as they are not supported in version 6 or over: https://www.elastic.co/guide/en/elasticsearch/reference/6.0/removal-of-types.html

The following, for example, should be removed:

```
document_type => "kubernetes"
```

If in doubt, check Management > Upgrade Assistant > Indices in Kibana, which was added in v5.6, or the deprecation messages in log output.
