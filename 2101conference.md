## [Devops 관점에서 본 마이크로서비스로의 여정](https://www.youtube.com/watch?v=xtiC8-SYmBg&list=PL42XJKPNDepZbqM9N11RxL5UY_5PbA_Wo&index=23&ab_channel=TOAST)

### Role

- spring cloud config server / gateway server 
- jenkins pipeline 
- cloud provisining
- manage docker container 
- monitoring

### MSA로 전환으로 고민

- 운영중인 쇼핑몰? 
- 개발과 테스트는 어떻게? 
- 방법
  - 마틴파울러 [strangler pattern]() 
    - proxy를 두어서 legacy, MSA 공존하게 한후, MSA가 정착되고 나서, legacy를 삭제한다. 
  - nginx docker 로 구성 
    - config 설정 
  - @Deprecated (컨트롤러)

### Note 

- 서버별 접속 편하게? 
  - Ansible로
- 배포 프로세스 
  - checkout
  - clean 
  - build
  - test
  - image(docker)
  - deploy
- 모니터링 
  - nginx 모니터링 
    - access log -> fluentd -> elasticsearch -> grafana 로 도식화 
      - 요청별 최대 응답시간 
      - 요청별 응답 코드 추이 (200, 400 HTTP status code)
  - 수많은 애플리케이션
    - 로그를 한군데 수집 후 -> 모니터링
    - docker -> grafana loki(plugin) -> grafana
  - 미들웨어
    - prometheus exporter 사용 
    - kafka, redis, gateway, mongo, zookeeper, nexus, neo4j
  - host와 docker 컨테이너 
    - host: prometheus node exporter 사용
      - 디스크 사용률, 메모리 사용률, cpu 사용률, 네트워크 트래픽
    - docker: c Advisor 사용
      - 서비스중인 컨테이너 수, 컨테이너별 CPU, 컨테이너별 메모리 사용률

- more 
  - canary 배포, blue/green 배포 

