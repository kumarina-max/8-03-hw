---
# Домашнее задание к занятию GitLab CI/CD  
**Марина Кукушкина**

## Задание 1: Развертывание GitLab и настройка runner

### Скриншот 1: Активный runner в проекте
![Runner active](images/runner.png)

### Скриншот 2: Настройки раннера
![Runner settings](images/runner-settings.png)

 
### Задание 2

### Файл .gitlab-ci.yml

```yaml
stages:
  - test
  - build
  - deploy

test_job:
  stage: test
  image: alpine:latest
  tags:
    - docker
  script:
    - echo "=== Запуск тестов ==="
    - echo "Проверяем окружение"
    - uname -a
    - echo "Тесты успешно пройдены!"

build_job:
  stage: build
  image: alpine:latest
  tags:
    - docker
  script:
    - echo "=== Сборка проекта ==="
    - mkdir -p build
    - echo "Результат сборки от $(date)" > build/info.txt
    - cat build/info.txt
  artifacts:
    paths:
      - build/
    expire_in: 1 week

deploy_job:
  stage: deploy
  image: alpine:latest
  tags:
    - docker
  script:
    - echo "=== Деплой ==="
    - ls -la build/ 2>/dev/null || echo "Артефакты готовы"
    - echo "Деплой успешно выполнен!"
  only:
    - main

Скриншоты успешных сборок

![Скриншот 1](images/pipeline-passed.png) ![Скриншот 2](images/test_job.png)

![Скриншот 3](images/build_job.png) ![Скриншот 4](images/deploy_job.png)

