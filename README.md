## ���˵�� (2016-04-25)

### ���ģ��

1. ��componentsĿ¼���½���Ӧ��ģ��, ���Ը���userģ��, �ĵ���Ӧ������.
2. ��js/_appModules.js�����Ӧģ��_references.js�ļ�
3. ��js/_appInitial.js���ض�Ӧ��ģ��


### sharedģ��˵��

1. ��ģ����һ������ģ��, �����˹�����service, filter, directives ..
2. ����ģ����԰�������ش�ģ��

### ģ��˵�� (js/componets/user)Ϊ��

1. ģ����router.jsΪ��ģ��ǰ��·��, ����·�ɶ������ڴ��ļ���
2. appUser.js ����ģ������

### ���jwt�����Զ�����token jwtInterceptor http������
1. token expire then refresh automatic

            /*
             * Jwt Interceptor
             * when token expire then refresh automatic
             */
            jwtInterceptorProvider.tokenGetter = function(jwtHelper, $http) {
                var jwt = $localStorageProvider.get('token');
                if(jwt){
                    if(jwtHelper.isTokenExpired(jwt)){
                        console.log('token is expired', jwt);
                        var apiUrl = GlobalConfig.apiConfig.host + '/' + GlobalConfig.apiConfig.endpoint;
                        var refreshTokenUrl = apiUrl + '/auth/refresh';
                        return $http({
                            url : refreshTokenUrl,
                            skipAuthorization : true,
                            method: 'GET',
                            headers : { Authorization : 'Bearer '+ jwt},
                        }).then(function(response){
                            var newToken = response.data.data.token;
                            $localStorageProvider.set('token', newToken);
                            return newToken;
                        },function(response){
                            $localStorageProvider.set('token', '');
                        });
                    }else{
                        return jwt;
                    }
                }

            }



