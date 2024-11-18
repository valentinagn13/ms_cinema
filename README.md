#En SECURITY CONTROLLER de ms_seguridad hay que tener un endpoint que desifre el token

        @PostMapping("/decode-token")
    public ResponseEntity<?> decodeToken(@RequestBody Map<String, String> requestBody) {
        String token = requestBody.get("token");
        User user = theJwtService.getUserFromToken(token);

        if (user != null) {
            Map<String, Object> response = new HashMap<>();
            response.put("_id", user.get_id());
            response.put("name", user.getName());
            response.put("email", user.getEmail());
            return ResponseEntity.ok(response);
        } else {
            return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Token inválido o expirado");
        }
