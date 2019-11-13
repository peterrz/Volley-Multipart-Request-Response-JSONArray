# Volley-Multipart-Request-Response-JSONArray


## Getting Started

Volley multipart request send data and files while the response is JSONArray

### Prerequisites

add volly to your build.gradle

```
implementation 'com.android.volley:volley:1.0.0'
```

### Installing

Copy the VolleyMultipartRequest class to your directory



```
VolleyMultipartRequest.java
```

And in your activity add this codes:

```
        //Our custom volley request
        VolleyMultipartRequest volleyMultipartRequest = new VolleyMultipartRequest(Request.Method.POST, allAdress,
                new Response.Listener<JSONArray>() {
                    @Override
                    public void onResponse(JSONArray response) {
               //...
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                   
                    //...
                  
                    }
                }) {

            /*
             * If you want to add more parameters with the image
             * you can do it here
             * here we have only one parameter with the image
             * which is tags
             * */
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                Map<String, String> params = new HashMap<>();

                params.put("name", name.getText().toString());

                return params;
            }

            /*
             * Here we are passing image by renaming it with a unique name
             * */
            @Override
            protected Map<String, DataPart> getByteData() {
                Map<String, DataPart> params = new HashMap<>();
                long imagename = System.currentTimeMillis();

                params.put("avatar", new DataPart(imagename + ".jpg", getFileDataFromDrawable(universal)));
                return params;
            }
            @Override
            public Map<String, String> getHeaders() throws AuthFailureError {
                Map<String, String> params = new HashMap<String, String>();
                params.put("X-Requested-With", "XMLHttpRequest");
                params.put("Authorization", "Bearer " + new PrefManager(getApplicationContext()).getToken());
           


                return params;
            }
  
        AppController.getInstance().addToRequestQueue(volleyMultipartRequest);

    }
```


