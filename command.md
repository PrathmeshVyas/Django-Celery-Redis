pip freeze > requirements.txt
docker-compose up -d --build
docker exec -it django /bin/sh

tp1.delay()

from celery import group
from cworker.tasks import tp1, tp2, tp3, tp4
task_group = group(tp1.s(), tp2.s(), tp3.s(), tp4.s())
task_group.apply_async()

from celery import chain
from cworker.tasks import tp1, tp2, tp3, tp4
task_chain = chain(tp1.s(), tp2.s(), tp3.s())
task_chain.apply_async()
