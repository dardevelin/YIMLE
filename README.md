#YIMLE
=========
Description: This script allows to have an easy double click access to the
    ISP(internet service provided) prefered cache video file,
    which allows watching/downloading videos that do not work
    with youtube.com/html5 mode.
    
#LICENSE

Copyright (C) 2012 - Darcy Brás da Silva

YIMLE is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version.

YIMLE is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with YIMLE. If not, see <http://www.gnu.org/licenses/>.


#USAGE
=========
bookmark the link bellow. After that, whenever you are on a youtube video
click it once, it will redirect you to the mobile version, click again
and should start downloading. Enjoy

[javascript:(
    function() 
    { 
	    _url = document.URL;
	    _url_len = _url.length;
	    _version = 0; /* 0 desktop, 1 mobile*/

	    /*check if in youtube*/
	    _status = _url.search("youtube.com");

	    if(_status === -1 )
	    {
	        /*not in youtube, exit*/
	        return;
	    }

	    /*find if in desktop or mobile version*/
	    if( _status - 2  >= 0 )
	    {
	        if(_url[_status - 2] === 'm')
	        {
		        _version = 1;
	        }
	    }

	    /*get video code*/
	    _status = 0;
	    _status = _url.search("v=");
	    if(_status != -1)
	    {
	        /*find end of video code*/
	        for(_pos = _status+2; _pos < _url_len && _url[_pos]!='&'; _pos++)
	        {
		        /*keep counting*/
	        }

	        /*get video code*/
	        _video_code = _url.substring(_status+2, _pos);

	    }
	    else
	    {
	        /*could not find video code*/
	        return;
	    }

	    if(_version === 0)
	    {
	        /*desktop version _ redirect to mobile page*/
	        _redir = "http://m.youtube.com/watch?v=" + _video_code;
	    }
	    else
	    {
	        /*mobile version _ redirect to download*/
	        /*get video src*/
	        _element = document.getElementById( ("player_" + _video_code) );
	        _redir = _element['src'];

	    }
	    window.open(_redir,'_self');

    })()]
