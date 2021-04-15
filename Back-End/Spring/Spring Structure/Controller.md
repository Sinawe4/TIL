# Controller(web)
- 해당 요청 url에 따라 적절한 view와 mapping 처리
- `@Autowired Service`를 통해 service의 method를 이용
- 적절한 ResponseEntity(DTO)를 body에 담아 Client에 반환
- EX 1)
    ```JAVA
    @Controller
    @RequestMapping("/")
    public class HomeController {
        @GetMapping
        public String home(HttpSession session) {
            if (!SessionUtil.getUser(session).isPresent()) {
                return "login";
            }
            return "index";
        }   
    }   
    ```
    - @Controller
        - API와 view를 동시에 사용하는 경우에 사용
        - 대신 API 서비스로 사용하는 경우는 @ResponseBody를 사용하여 객체를 반환한다.
        - view(화면) return이 주목적
- EX2)
    ```JAVA
    @RestController
    @RequestMapping("/api/users")
        public class ApiUserController {
        @Autowired
        private UserService userService;

        @PostMapping("/login")
        public ResponseEntity login(@RequestBody @Valid LoginDto loginDto, HttpSession session) {
            SessionUtil.setUser(session, userService.login(loginDto));
            return new ResponseEntity(HttpStatus.OK);
        }
    }
    ```
    - @RestController
        - view가 필요없는 API만 지원하는 서비스에서 사용 (Spring 4.0.1부터 제공)
        - @RequestMapping 메서드가 기본적으로 @ResponseBody 의미를 가정한다.
        - data(json, xml 등) return이 주목적: return ResponseEntity
        - 즉, @RestController = @Controller + @ResponseBody