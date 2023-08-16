

## 간단하게 기존 코드에 validation 추가하는 방법

예를 들어 social link 에 http:// , https:// 형태의 유효성 검증이 필요하다고 요청일 들어올 경우에 간단하게 State 로 validation 을 처리할 수 있다.

```ts
 const [regSocialBoolean , setRegSocialBoolean] = useState(true);

```

state 로 검증했을 때 상태 값을 만들어 주고

```ts
    useEffect(() => {
        if (!regURL.test(formVariable?.social_link?.toString() as string)){
            if (formVariable.social_link?.toString() === "")
                setRegSocialBoolean(() => true)
            else
                setRegSocialBoolean(() => false)
        }else {
            setRegSocialBoolean(() => true)
        }
    } , [formVariable.social_link])

```
훅으로 사용하는 value 값이 변경 될 때 마다 검증할 수 있또록 useEffect 를 설정해준다.

그런 다음 view 로 boolean State 를 넘겨준 다음

```ts
        <StepOneView
            formVariable={formVariable}
            onChangeVariable={onChangeVariable}
            setFileHandler={setFileHandler}
            handleNextButton={handleNextButton}
            regEmailBoolean={regEmailBoolean}
            regSocialBoolean={regSocialBoolean}
        />
```

이런 형태로 삼항 연산자를 사용해서 처리한다.

```ts
       <div className="inp_wrap">
          <div className={!regSocialBoolean ? `inp_box err` : "inp_box"}>
              <div className="label">
                  <label htmlFor="org_link">{t("socialLink")}</label>
              </div>
              <div className="inp">
                  <input
                      type="text"
                      name="social_link"
                      id="org_link"
                      placeholder="Homepage, Blog, SNS, etc."
                      value={formVariable.social_link}
                      onChange={onChangeVariable}
                  />
              </div>
          </div>
          {!regSocialBoolean && (
              <div className="err_box">
                  <span className="msg">{!regSocialBoolean && "Please enter in URL format. ex) http://your social link , https://your social link"}</span>
              </div>
          )}
      </div>
```

이 프로젝트는 퍼블리싱을 받아 처리했기 때문에 scss 가 아닌 class 형태로 처리하였다는 점을 참고해주세요.
