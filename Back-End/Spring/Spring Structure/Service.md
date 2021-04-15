# Service
- `@Autowired Repository`를 통해 repository의 method를 이용
- 적절한 Business Logic을 처리한다.
- DAO로 DB에 접근하고 DTO로 데이터를 전달받은 다음, 비지니스 로직을 처리해 적절한 데이터를 반환한다.  
- EX)
    ```JAVA
    @Service
    public class UserService {
        @Autowired
        private UserRepository userRepository;
        @Resource(name = "bCryptPasswordEncoder")
        private PasswordEncoder bCryptPasswordEncoder;
        @Autowired
        private MessageSourceAccessor msa;

    public User save(UserDto userDto) {
        if (isExistUser(userDto.getEmail())) {
           throw new UserDuplicatedException(msa.getMessage("email.duplicate.message"));
        }
        return userRepository.save(userDto.toEntityWithPasswordEncode(bCryptPasswordEncoder);
        }   
    }
    ```