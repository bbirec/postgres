AWS RDS에서 Postgres를 쉽게 호스팅 할 수 있으며, DB관리 측면에서 편한 기능을 많이 제공한다.

## DB 생성
직접 Linux서버에 접속해서 설치하고, 설정해줄 필요없이 AWS console에서 DB사양과 몇가지 설정만으로 바로 DB를 생성할 수 있다.

- **Multi-AZ** -
실제 서비스하는 용도의 DB라면 *Multi-AZ* 옵션을 켜야 한다. 이 기능은 같은 데이터센터내에 동일한 DB서버를 하나 더 만들어 두고, 
하드웨어 에러나 여러가지 에러 상황에서 Stanby하고 있는 서버로 바꿔주는 기능을 한다. DB를 재부팅, 시스템 업데이트 등등
시간이 오래 걸리는 작업도 Downtime을 1분이내로 해줄 수 있는 기능이다.

- **Disk** - 
일반적으로 *General Purpose SSD*를 사용하며, Disk Size에 따라 IOPS가 설정된다. 따라서 더 높은 IO가 필요하다면 실제 
사용하는 Disk 크기보다 크게 설정한다. 

Storage size (GB) | Base performance (IOPS) | Maximum burst duration @ 3,000 IOPS (seconds) | Seconds to fill empty credit balance
------------------|------------------------|------------------------------------|------------
| 1 | 3	| 1,802 | 1,800,000 |
| 100 | 300 | 2,000 | 18,000 |
| 250 | 750 | 2,400 | 7,200 |
| 500 | 1,500 | 3,600 | 3,600 |
| 750 | 2,250 | 7,200 | 2,400 |
|1,000|3,000 | Infinite | N/A |

Disk에 대한 더 자세한 설명은 [여기](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html)에서 확인 가능하다.

- **Maintenance Window** - 
Postgres DB 업데이트나 Reboot이 필요한 경우 정해진 시간에 자동으로 실행되게 하는 옵션이다. DB 설정을 바로 수정할 필요가 없는 경우 
새벽 시간대에로 window를 설정해두면 그 시간에 자동으로 설정을 변경하고 재부팅 된다.

## IOPS
*Input/Output Operations Per Second* 이라는 뜻으로 초당 IO Read/Write를 얼마나 하는가에 대한 수치를 나타낸다. 

RDS 인스턴스를 생성할때 정하는 IOPS는 얼마만큼의 IOPS까지 가능한지를 정하는 것이고, 아무리 DB 인스턴스 사양(cpu, memory)이
좋더라도 IOPS가 낮으면 쿼리가 느리게 실행되는 것을 경험할 수 있다.

높은 IOPS로 설정하면 할수록 비용이 많이 비싸기 때문에 적은 IOPS로 먼저 설정해 두고 사용하는 IOPS를 모니터링 하면서 
현재 서비스에 맞게 IOPS를 조정해 나가야한다.

## Read Replica
AWS RDS를 사용하는 여러가지 이유 중에 Read replica를 쉽게 생성하고 관리할 수 있다는 점이 있다. 만약 DB에서 통계를 내거나 
하는 등의 많은 CPU를 요구하는 작업을 실제 서비스 DB(Master)에서 하는것이 아니라 동일하게 복사된 서버인 Read Replica(Slave) 
서버에서 함으로써 서비스 DB의 부하를 주지 않으면서 원하는 작업을 할 수 있다.

Read Replica를 생성하면 자동으로 변경 사항을 복제하며, 당연히 Write operation은 할 수 없다. Master DB에서 갑자기 많은 양의 
변경 사항이 있거나, Read Replica 서버에 문제가 있는 상황에서 `Replica Lag`가 발생하게 되는데 이 수치를 낮게 유지하도록 해야 한다.