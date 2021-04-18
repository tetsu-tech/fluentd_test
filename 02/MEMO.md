```sh
docker run --rm -d --name=rec_tail_file_fluentd --expose 24224 -v `pwd`/.:/fluentd/etc -v `pwd`/.:/tmp/log fluent/fluentd:edge-debian -c /fluentd/etc/receiver_tail_file.conf

docker run --rm -d --name=sender_tail_file_fluentd --link rec_tail_file_fluentd -v `pwd`/tmp/etc:/fluentd/etc -v `pwd`/tmp/log:/tmp/log fluent/fluentd:edge-debian -c /fluentd/etc/sender_tail_file.conf


echo "test" >> tmp/log/sender_tail_file.log
cat ./tmp/log/receiver_tail_file.20210418.log
```
