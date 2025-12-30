# Class Validator



## Class Validator 와 DTO 사용하기 \~ PickType 활용

`yarn add class-validator`

```javascript

export class CreatePostDto {
    @IsString()
    title: string;
    
    @IsString()
    content: string;
}


export class UpdatePostDto {
    
    @IsString()
    title: string;
    
    @IsString()
    content: string;
}
```

위와 같이 request dto 를 만들 수 있습니다.

하지만 만약에 title 과 content 를 다른곳에서 사용하고 있다고 하면 조금 더 간단하게 코드를 작성할 수 있습니다.



```javascript
export class UpdatePostDto extends PickType(CreatePostDto ,['title','content']) {

}
```
