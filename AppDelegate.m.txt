/**
 * Note: the following function should already exist in your application delegate file.
 * Replace it with the following implementation.
 *
 * Thanks to @purplecabbage for implementation.
 * Thanks to Ruddiger for the iFrame patch.
 */

// ...

/**
 * Start Loading Request
 * This is where most of the magic happens... We take the request(s) and process the response.
 * From here we can re direct links and other protocalls to different internal methods.
 */
- (BOOL)webView:(UIWebView *)theWebView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType
{
	NSURL *url = [request URL];
	
	// Intercept the external http requests and forward to Safari.app
	// Otherwise forward to the PhoneGap WebView
        // Avoid opening iFrame URLs in Safari by inspecting the `navigationType`
	if (navigationType == UIWebViewNavigationTypeLinkClicked && [[url scheme] isEqualToString:@"http"] || [[url scheme] isEqualToString:@"https"]) {
		[[UIApplication sharedApplication] openURL:url];
		return NO;
	}
	else {
		return [ super webView:theWebView shouldStartLoadWithRequest:request navigationType:navigationType ];
	}
}