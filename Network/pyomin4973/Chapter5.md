- 5.2 Routing Algorithms(LS,DV)
    - 포워딩 테이블의 엔트리를 채우기 위해 routing 알고리즘 사용. 포워딩 테이블에 적히는 것은 destination에 대해서 next가 ouput link가 누군지에 대해 적혀있다.
    - 알고리즘을 통해 최소 경로를 구할 수 있다.
    - 구한 최소경로로 도달하기 위해 방문해야되는 곳을 알게된다. destination이 A일때 어디로 가야 최소로 갈 수 있는 지를 포워딩테이블에 채울 수 있게 된다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/3ea1ab8f-f25b-460b-8bc5-60905baa99aa/Untitled.png)
    

- 5.3 Intra-AS Routing in the Internet
    - AS: Autonomous Systems(자체적 시스템), An autonomous system is an autonomous routing domain that has been assigned an Automous System Number(ASN) 대학교 등은 AS이기 때문에 자체 시스템에서 어떤 라우팅 알고리즘을 사용할 지 등은 자치적으로 정함. globally unique한 AS 번호가 있다. Harvard는 11번이다.
    - AS들끼리 연결되어 있다. AS는 네트워크기관 ISP라고도 불림(Internet service provider). AS는 인터넷 서비스를 제공하면서 돈을 번다. AS와 AS간에도 서비스를 제공받고 대가를 지불하기도 한다. (KT- 대학교: KT의 회선을 사용하면서 비용을 지불한다. 이때 kt는 갑이고 대학교는 을) 그래서 밑의 검정선과 같은 관계는 없는데 비용을 지불하기 어렵기 때문이다. (구름은 각 AS들)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/afa175ac-2092-48d6-81a4-4dc0b215cf4a/Untitled.png)
    
    - 체급이 비슷한 둘다 서로가 필요한 관계는 Peering relationship. peer가 되면 두개 사이의 회선에서 왔다갔다하면서 무료로 서비스를 주고받기도 함. (동등관계) Peers do not provide transmit between peers.
    - 관계들은 비공개 → 기업의 위상이 보여지기 때문에(갑을 관계)
- 5.4 Routing Among the ISPs: BGP (Border Gateway Protocol)
    - policy-based 라우팅 프로토콜이다.(AS간 관계 구현을 위함.)
    - de facto EGP of today’s global Internet
    - Relatively simple protocol, but configuration is complex and the entire world can see, and be impacted by your mistakes
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/f41a4f16-47f3-49bd-8cc5-62ed0629a26e/Untitled.png)
    
    - BGP는 inter AS routing protocol이고 AS의 가장자리에 있는 gateway 라우터들끼리 대표로 이루어지는 일이다.
    - BGP의 작동방식
        - 우선 내 prefix가 어딨는지 알려줘야 한다. 어딨는지 알고 찾아올 수 있도록 BGP 메세지에 담아서 다른 AS한테 보내야 한다. 어떤 방향에 이 prefix가 있는지를 계속해서 퍼뜨림. 퍼뜨릴 때 AS Path에 자기자신에 대한 AS정보도 추가시킴. → 어떤 방향에서 온지 알 수 있도록.
        - 밑의 예시에서는 삼성이 2개의 정보를 받는데 두쪽으로 모두 갈 수 있음을 알 수 있다. 두 방식 둘다 4개를 거쳐서 갈 수 있음도 알 수 있다. 여기서 구글로 보내기 싫은 경우에 (정책적 선택으로) AS 정보 보고 위의 방향으로 보낼 수도 있다. 빨리만 보내고 싶은 경우에, 경로가 짧은 걸 고르는 경우가 많다.
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/1715ad90-82ad-45eb-b0b5-3e9de95da08c/Untitled.png)
            
        - 본인한테 돈이 되는 데이터만 운반한다. 같은 곳으로 보낼때 경로가 많으면 기왕이면 customer에게 보내는 것을 먼저 보내는 선택을 하는 경우가 있다. 돈을 벌기위해서 (enforce order of route preference: Customer>Peer>Provider)
        - AS 1이 reachability information을 보내는 경우. 한양대학교는 AS 1에 도달하는 경우가 3개있음을 알 수 있다. AS의 관계를 따졌을때 밑으로 보내는 경우가 많다. 위로 가면 돈 내야하고 중간으로하면 돈 안내고 밑으로가면 돈을 번다. 더 오래 걸리긴해도..
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/d9d38d23-ab7c-4737-afeb-54f7b78db30a/Untitled.png)
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/91b5bb19-221e-4996-8b50-88e3f00c3a64/53d94fe3-f13e-4d58-ac7c-33f5e494dd48/Untitled.png)
        
        - inter-AS: admin wants control over how its traffic routed, who routes through its net. can focus on performance자신의 트래픽이 어떻게 경로 설정되는지와 누가 그 네트워크를 통해 경로를 설정하는지를 통제하고자 하며, 성능에 중점을 두고 있습니다.
        - intra-AS: single admin, so no policy decisions needed. policy may dominate over performance 단일 관리자이므로 정책 결정이 필요하지 않습니다. 정책이 성능보다 우선될 수 있습니다.
            - OSPF routing은 intra-AS routing에서 사용된다. OSPF는 Open Shortest Path First의 약자로 link state 프로토콜이다. 다익스트라 least-cost path 알고리즘과 link-state 정보가 흘러갈 때 사용한다. 라우터는 AS의 모든 다른 라우터에게 라우팅 정보를 broadcast한다. 라우터는 링크 state에 변화가 있을때마다 link-state의 정보를 broadcast한다. 또 변화가 없을 때에도 link의 state를 주기적으로 broadcast한다.
            
            - OSPF는 링크 가중치가 설정된 정책을 만들지 않고 대신 가장 cost가 적은 path로의 routing을 결정하는 메커니즘을 제공한다.
