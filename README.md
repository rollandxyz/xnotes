# xnotes
My notes

https://github.com/jasonaden/angular-cli-lib-example
https://semver.org/
https://gitversion.readthedocs.io/en/latest/more-info/version-increments/


https://coursetro.com/posts/code/132/Material-Design-Bootstrap-4-and-Angular-5-Tutorial---MdBootstrap
https://mdbootstrap.com/angular/components/#
https://ng-bootstrap.github.io/#/getting-started

<code>
    public class ArcGISRest
    {
        
        static string urlRoot = "http://geocode.arcgis.com/arcgis/rest/services/World/GeocodeServer/findAddressCandidates";
        static HttpClient client = new HttpClient();
        public static async Task<string> FindAddressCandidatesAsync()
        {
            string url = urlRoot;
            url += "?Address=380+new+york+st";
            url += "&City=redlands";
            url += "&Postal=92373";
            url += "&outFields=*";
            url += "&forStorage=false";
            url += "&f=pjson";

            string product = null;
            HttpResponseMessage response = await client.GetAsync(url);
            if (response.IsSuccessStatusCode)
            {
                product = await response.Content.ReadAsStringAsync(); // .ReadAsAsync<string>();
            }
            return product;
        }

        public static string FindAddressCandidates()
        {
            string url = urlRoot;
            url += "?Address=380+new+york+st";
            url += "&City=redlands";
            url += "&Postal=92373";
            url += "&outFields=*";
            url += "&forStorage=false";
            url += "&f=pjson";

            using (var httpClient = new HttpClient())
            {
                httpClient.DefaultRequestHeaders.Add("User-Agent", "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36");
                var response = httpClient.GetStringAsync(new Uri(url)).Result;
                return response;
            }
        }
    }
    
    private void toolStripButton1_Click(object sender, EventArgs e)
        {
            richTextBox1.Text = "";
            richTextBox1.BackColor = Color.Orchid;
            richTextBox1.Text = ArcGISRest.FindAddressCandidates();
        }

        private async void toolStripButton2_Click(object sender, EventArgs e)
        {
            richTextBox1.Text = "";
            richTextBox1.BackColor = Color.PaleGreen;
            var a = await ArcGISRest.FindAddressCandidatesAsync();
            richTextBox1.Text = a;
        }
        
    </code>
    
    
