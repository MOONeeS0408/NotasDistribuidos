# NextAuth

Una de las mejores formas y mas sencillas para autenticar, usando React.

Ventajas del framework:



* Ayuda en el ruteo \<Route>, con ruteo basado en archivos, eso ya no se necesita codificar, lo realiza en base a los directorios.&#x20;
* Permite realizar la Module Federation

{% embed url="https://next-auth.js.org" %}

LDAP

open LDAP

idM

Active Directory

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Mantener usuarios fuera de la base de datos a alguien que ya lo gestiona.

* Single Sign-On (SSC), token que se da por la vida de tu sesión. Si revisa y el token aun es valido la sesión se mantiene abierta. Ejemplos: Kerberos, Keyclock

1. Request/Access Token: Request a un servidor de autenticación,&#x20;
2. Verify Client: se verifica que el cliente sea valido.&#x20;
3. User Consent: Si existes, entonces&#x20;
4. Return Access Token
5. Rquest resourse: Ahora si permite que el usuario entre
6. Validate Token: Según los privilegios que tenga el usuario sobre cada recurso. Los privilegios se dan por <mark style="color:red;">**RBAC**</mark> <mark style="color:red;"></mark><mark style="color:red;">(Role Based Access Control): Control de acceso basado en roles.</mark> Rol: permisos asumidos como usuarios. Asignar roles especificos a un usuario o grupo de usuarios.&#x20;
7. Valid Token
8. Returns Rsource



¿Como implementar en un codigo de React?

Cualquier plugin que quisieramos ingresar se debe colocar en la linea 3, Recordar que para instalar se usar npm install @react-oauth/google o nombre del plugin



PRoveedor y login



{% embed url="https://cloud.google.com/cloud-console?utm_source=google&utm_medium=cpc&utm_campaign=latam-MX-all-es-dr-SKWS-all-all-trial-b-dr-1605194-LUAC0020230&utm_content=text-ad-none-any-DEV_c-CRE_654757056926-ADGP_Hybrid%20%7C%20SKWS%20-%20BRO%20%7C%20Txt%20~%20Management-Tools_Console-KWID_43700076071300681-kwd-300738725413&utm_term=KW_cloud%20console-ST_Cloud%20Console&gclid=Cj0KCQjw7JOpBhCfARIsAL3bobcY6olHrMfABfB0A1OvSe-zjyLcxU6Wl5PKo5gHLkp2fdQPq-rvOCoaAly8EALw_wcB&gclsrc=aw.ds&hl=es-419" %}

Console >  API > crear neuvo prouecot

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Entrr a configurar



EXternos







<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>



Autenticaión basada en Json,&#x20;

Petición al servidor de un token, permite decificar, se tiene que instalar

```
import jwt_decode from 'jwt-decode';
```



UseNavigate

despues de una direccion, te manda a otra direccion



Nueva funcion, home, linea 13

```javascriptreact
function Home({ userData, setUserData }) {
  const navigate = useNavigate();
```



REvocion, quitar datos, para ver que no podemos acceder el contenido, para hacer el sign out

```javascriptreact
 const handleSignOut = () => {
    localStorage.removeItem('jwtToken'); //Remueve el token
    setUserData(null);
    navigate('/'); //nos redirige al home.
  };
```

Linea 27 realiza la validacin del usuario,&#x20;



Error&#x20;

4XX error del cliente , 4??

5XX error del desarrolador, 5??





Linea 57 para&#x20;

```javascriptreact
      <GoogleOAuthProvider clientId='814023381285-pi3pebsurmir2nu64mdvgodksfvruenv.apps.googleusercontent.com'>
        
```

Kubernetes, esto se realiza en un secret, obtenida con  fsbld entorno.&#x20;



variabl que ya existe, i¿oni



```javascriptreact
onst [userData, setUserData] = useState(null);
```

Todo console.xxxx es el logeo

```javascriptreact
console.error('Error decoding JWT token', error);
```

EStos mensajes aparecen al inspeccionar el codgio.  LINEA 79

Primero cacha el string y luego el mensaje.&#x20;

linea 83 HAndle Error



USE EFFECT  linea 89

busca el error&#x20;





return linea 100, manejo de rutas.





{% embed url="https://nextjs.org" %}

Framework que usaremos de ahora en adelante para el proycto.

&#x20;\|-----> Module Federation



Ayuda en la parte de ruteo





NExt.js + NextAuth

Ayuda en proveedores?

Solo es verificar el proveedor que nos toca.&#x20;





