---
---
CSAPP의 Architecture Lab에 대한 솔루션입니다.

## 환경 구성
본 과제에서 y86-64 머신 시뮬레이션을 위해 GUI tool을 제공한다. 이 tool을 빌드하기 위해 tk, tcl, tk-dev, tcl-dev 패키지들이 필요하다. 다음 명령어를 통해 설치해주도록 한다.

* 필요한 패키지 설치  

	```bash
    sudo apt install tcl tcl-dev tk tk-dev
    sudo apt install flex
    sudo apt install bison
	```
    
* build error

    최신 리눅스 머신인 경우 위 명령어로 설치하면 tk, tcl 버전이 8.6 이상이다. 과제에서 제공하는 tool의 소스코드는 8.5 버전을 기반으로 짜여졌다. 해당 버전이 바뀌면서 객체 구조가 좀 바뀌어서 빌드가 안되는데 아래와 같이 조치하여 빌드하도록 한다.
    ```bash
    # 아래와 같이 모든 interp->result 구조를 사용하는 코드를 변경한다.
    interp->result = "No arguments allowed"     =>  Tcl_SetResult(interp, "No arguments allowed", TCL_STATIC);
    fprintf(stderr, "Error Message was '%s'\n", sim_interp->result);   =>     fprintf(stderr, "Error Message was '%s'\n", Tcl_GetStringResult(sim_interp));
    ```
