# 7세그먼트 자리 스캔 · LAB2

학생용 시작점은 빈 템플릿 v2.0.0이다. 이 폴더는 강사용 완성 코드 예시를 제작 중인 작업본이다.

```powershell
git clone --branch v2.0.0 https://github.com/Glaysia/fpga-lab-template.git lab2_08_segment_scan
cd lab2_08_segment_scan
git switch -c main
code LAB1.code-workspace
```

기능 코어: `segment_scan8` / Vivado 설계 top: `lab2_segment_scan` / 시뮬레이션 top: `tb_segment_scan8`.

- `src/segment_scan8.v`: 직접 학습하는 회로.
- `src/input_frontend.v`: 리셋 해제 동기화, 두 단계 입력 동기화, 20 ms 버튼 디바운스와 한 클록 펄스.
- `src/lab2_segment_scan.v`: 입력·출력을 코어와 보드 핀 이름에 연결.
- `sim/tb_segment_scan8.sv`: 기능 코어의 자기검사. 보드 핀 검증과 구분한다.
- `constraints/lab2_segment_scan.xdc`: 35개 포트, S75 핀과 LVCMOS33, 1 kHz 주 클록 제약.

장비 설정: 주 클록을 **1 kHz**로 설정하고 초기화 버튼 K4를 누른 뒤 놓는다. 버튼 N8은 클록이 아니라 입력이다. 스위치를 먼저 정하고 버튼을 누른다.

SW1..4(sw[7:4]): 첫 자리 숫자. COM[7]부터 입력값,1,2,3,4,5,6,7 순서. 1 kHz에서 자리당 62.5 Hz, blanking 포함.

입력 동기화 때문에 버튼과 DIP 입력은 즉시 반영되지 않는다. 버튼은 누름과 뗌 모두 충분한 안정 시간이 필요하다. 기계적 접점과 메타안정성의 실제 특성은 기능 시뮬레이션만으로 증명하지 않는다.

실행: Terminal → Run Task... → 02 Simulate. 보드 연결 검증 및 실제 장치 실행 상태는 상위 LAB2 검증 기록을 확인한다.
