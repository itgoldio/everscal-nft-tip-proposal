ссылки

Etehreum EIP 721 https://eips.ethereum.org/EIPS/eip-721

Solana v1.2.0 https://docs.metaplex.com/token-metadata/specification


# Abstract

Данный стандарт описывает дефолтный API для NFT. Каждый NFT является отдельным смартконтрактом и содержит:

- информацию о владельце
- логику передачи этого токена
- информацию о чтение данныъ этого токена

# Motivation

Стандартный интерфейс позволит испольховать NFT токен разными приложениями, маркетплейсами, кошельками, играми и многое другое.


# Specification

The keywords “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

# NFT root

Будет описано позже.

**NFT root** это смарт контракт который

- позволяет получить информацию о том, является ли токен коллекцие, или одиночным токеном
- позволяет получить информацию о коллекции
- верифицирует автора коллекции
- позволяет проводить быстрый поиск коллекции в БЧ
- позволяет продовать NFT
- позволяет реализовать логику по отложенному минтингу
- позволяет реализовать логику MrBox
- Управялет Semi Fungible токенами
 


# NFT

Возвращает адрес смартконтракта управляющего этим NFT

**getOwner**

```
function getOwner() external responsible returns(address addrOwner);
```


**getRoot**

Возвращает адрес смартконтракта создавшего данный токен

```
function getRoot() external responsible returns(address addrRoot);
```


**transferOwnership**

Передаёт токен новому владельцу.

Предлагаю стандартизировать funcId и первый параметр address addrTo  (но есть минус что тогда не работает TIP6 нормально)

```
function transferOwnership(
    address addrTo,
    address sendGasToAddr, 
    mapping(address => CallbackParams) callbacks
) external;

struct CallbackParams {
    uint128 value;
    TvmCell payload;
}

```

**getNftData**

Возвращает информацию о том что хранит NFT и как хранит.

- Дата создания
- Дата изменения данных (???)
- Размер
- MIMETYPE 
- Где храним (Enum)
- - Url
- - WorkChain

**getPermissions**

По аналогии с доступом к файлу, возвращаем кто может файл менять, удалять.

По ролям тут "Владелец", "Root (автор)"

