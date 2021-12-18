## 내가 짠 API

**Login**

    Method : POST 
    URL : {baseURL}/logIn

    Req: 
        header:
        body:ID, Password
    Res:
        200

**Logout**

    Method : GET
    URL : {baseURL}/logOut

    Res : return


**SignIn**

    Method : POST
    URL: {baseURL}/signIn 

    Req:
        header:
        body: id, pass, username,useremail, userimg
    
    Res: 201

<hr/>

## Ellie가 짠 API

**User Schema**

    {
        id: string //사용자의 고유한 아이디
        username: string, // 사용자 닉네임
        password:string, //사용자 비밀번호
        name: string, //사용자 이름
        email: string, //사용자 이메일
        url: string (optional) //사용자 프로필 사진
    }

**POST/auth/signup**

    Req:
        {
            username,
            password,
            name,
            email,
            url
        }
    Res:
        {
            token,
            username
        }

**POST/auth/login**

    Req:
        {
            token,
            password
        }

    Res:
        {
            token,
            username
        }

**GET/auth/me**

    {
        token,
        username
    }
    //기존 토큰이 유효하지 않은 지 확인하는 API