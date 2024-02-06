```java
    @GetMapping(value = "/pdf/inputstream", produces = MediaType.APPLICATION_PDF_VALUE)
    public ResponseEntity<InputStreamResource> streamResourcePdf() throws FileNotFoundException {
        File file = new File("/Users/yeonsigjang/Desktop/refactoring/한글은불가능한가요?.pdf");
        InputStream fileInputStream = new FileInputStream(file);
        return ResponseEntity.ok(new InputStreamResource(fileInputStream));
    }
```
- 직접 파일을 읽어서 fileInputStream으로 파일을 읽어서 리턴한다.
- 특별하게 header를 지정하지 않아도 open된다.
- 파일경로에 한글이 있어도 스트림으로 읽혀지기 때문에 파일 경로의 인코딩이 중요하지 않다.

```java
    @GetMapping("/pdf/open")
    public ResponseEntity<UrlResource> openPdf() throws MalformedURLException {
        UrlResource resource = new UrlResource("file:/Users/yeonsigjang/Desktop/refactoring/"+URLEncoder.encode("한글은불가능한가요?.pdf", StandardCharsets.UTF_8));
        return ResponseEntity.ok()
                .header(HttpHeaders.CONTENT_DISPOSITION, "inline; filename=refectoring.pdf")
                .header(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_PDF_VALUE)
                .body(resource);
    }
```
- header에 inline으로 처리한다.
- 리턴타입을 지정해준다.
- UrlResource
	- URL에서 리소스를 생성하기 때문에 파일 이름 부분의 URL 인코딩이 중요하다. **한글 경로가 있을경우 Encode처리가 필요함**

```java
    @GetMapping("/pdf/download")
    public ResponseEntity<UrlResource> downloadPdf() throws MalformedURLException {
        return ResponseEntity.ok()
                .header(HttpHeaders.CONTENT_DISPOSITION, "attachment; filename=refectoring.pdf")
                .body(new UrlResource("file:/Users/yeonsigjang/Desktop/refactoring/한글은불가능한가요?.pdf"));
    }
```
- 파일을 다운로드하는법

```html
        <a href="/pdf/inputstream" target="_blank">Inputstream</a>
        <a href="/pdf/open" target="_blank">Open</a>
        <a href="/pdf/download" target="_blank">Download</a>
```
- issue
	- 그냥 open하면 현재탭에서 오픈된다
	- 리턴할때 처리하는 방법은 찾지 못했고 링크를 오픈할때 `target="_blank"`를 주는식으로 새탭으로 띄울수 있다.