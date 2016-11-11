# MVW framework없이 Single Page App 만들기 5

***

## 다국어 지원 및 입력 유효성 검사

 - 다국어 지원을 위하여 jquery.li18n 라이브러리를 사용하였다.
 - 정규표현식을 통한 입력 유효성 검사를 구현하였다.
 
##### 1. jquery.li18n에 단어별 ID를 등록하고 사용한다. 

        $.li18n.translations = {
            eng: {
                strId_login : 'Login',
                strId_logout : 'Logout'
            },
            kr: {
                strId_login : '로그인',
                strId_logout : '로그아웃'
            }
        };
        $.li18n.currentLocale = 'eng';
        
        /* _t('strId_login') or $.li18n.translate('strId_login')로 사용 */
    
##### 2. Util에 IP Address 및 Url 등의 입력 유효성 검사 function을 구현하였다. 

    /* IP Address Check */
    hx.util.checkIpAddr = function(value) {
        var pattern = /^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$/;
        return pattern.test(value);
    };
    
    /* Url Check */
    hx.util.checkUrl = function(value) {
        var pattern = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w_\.-]*)*\/?$/;
        return pattern.test(value);
    };