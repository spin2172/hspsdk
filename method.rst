.. raw:: pdf

   PageBreak

.. _method:

======================================================
Method 목록
======================================================

OvenPlayer SDK for Android를 사용하기 위한 **public OvenMediaPlayer** Class 를 제공하며, 이 Class의 Method를 나열합니다.

setDataSource
------------------------------------------------------

.. function:: void OvenMediaPlayer::setDataSource(String uri) 
	
	재생할 미디어 URI를 설정합니다.

	:param String uri: 미디어 스트림 주소 또는 로컬 경로

	:rtype: void

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setDataSource("http://server.com/vod/playlist.m3u8");

getDataSource
------------------------------------------------------

.. function:: String OvenMediaPlayer::getDataSource()
	
	설정한 미디어의 URI값을 문자열로 반환합니다.

	:rtype: String
	:return: 설정한 미디어의 URI 값

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);
		String url = mMediaPlayer.getDataSource();

setStartPosition
------------------------------------------------------
.. function:: void OvenMediaPlayer::setStartPosition(Int startPos)
	
	기본적으로 OvenPlayer는 모든 미디어를 재생시 0초부터 재생하게 되어 있습니다. setStartPosition은 ‘이어보기’와 같은 기능을 제공할 경우 특정 위치부터 재생할 수 있도록 시작 위치를 지정해주는 메소드입니다. 반드시 Prepare() 메소드 이전에 설정이 되어 있어야 합니다.

	:param Int startPos: 재생 시작 시간, 단위 ms

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);
		...
		// 30초부터 재생함
		mMediaPlayer.setStartPosition(30000);

prepare
------------------------------------------------------
.. function:: void OvenMediaPlayer::prepare()
	
	setDataSource로 설정한 미디어 URI가 재생 가능한지 여부를 판단하고 재생을 할 수 있도록 모든 자원을 준비합니다. 이 메소드를 호출 한 뒤에 onPrepared 이벤트로 준비 완료 여부를 알 수 있습니다. onPrepared를 통해 준비 완료 이벤트를 받으면 재생 가능한 상태가 됩니다.

	.. note::
		prepare의 결과 이벤트를 :ref:`setOnPreparedListener` 를 통해 콜백 받을 수 있습니다. 
	
	
	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);
		...
		// 30초부터 재생함
		mMediaPlayer.prepare();

		// 준비 완료 이벤트 리스너
		OvenPreparedListener mPreparedListener = new OvenPreparedListener() {
			public void onPrepared(OvenMediaPlayer t, boolean result) {
				// Preparing이 성공하면 자동으로 재생함
				if(result==true){
					Log.d(TAG, String.format("Video Resolution: %d/%d",
							mMediaPlayer.getVideoWidth(), 
							mMediaPlayer.getVideoHeight()));
					mMediaPlayer.start();
				}
			}
		};

Play
------------------------------------------------------
.. function:: void OvenMediaPlayer::start()
	
	prepare 가 성공한 후 사용할 수 있으며 미디어 재생을 시작하는 메소드입니다. 준비 완료 여부는 onPrepared 이벤트를 통해 알 수 있습니다. 이 메소드를 호출하면 onBuffering 이벤트를 통해 버퍼링 상태를 알려주며, 버퍼링이 완료되면 재생을 시작합니다.

	:rtype: void

	.. note::
		start 호출 후 버퍼링 상태 이벤트를 :ref:`setOnBufferingUpdateListener` 를 통해 콜백 받을 수 있습니다. 

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);;

		mMediaPlayer.setDataSource("http://server.com/vod/playlist.m3u8");
		mMediaPlayer.prepare();
		mMediaPlayer.start();

		// 버퍼링 업데이트 이벤트 리스너
		OvenBufferingListener mBufferingUpdateListener = new OvenBufferingListener() {
			public void onBuffering(OvenMediaPlayer t, int percent) {
				Toast.makeText(getApplicationContext(),
					String.format("Buffering : %d%%", percent),
					Toast.LENGTH_SHORT).show();
			}
		};

pause
------------------------------------------------------

.. function:: void OvenMediaPlayer::pause()

	재생을 일시 중지 합니다. 재생 중이 아닌 상태에서 호출하면 아무 동작도 하지 않습니다.

	:rtype: void

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);
		...
		mMediaPlayer.pause();

stop
------------------------------------------------------

.. function:: void OvenMediaPlayer::stop()

	재생을 완전히 중지하고 스트림을 정리합니다. stop 함수를 호출한 뒤에는 start 함수를 호출하더라도 다시 재생되지 않으며, 미디어를 재생하기 위해서는 prepare 부터 다시 호출해야 합니다.

	:rtype: void

	``예제``

	.. code-block:: java

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this);
		...
		mMediaPlayer.stop();

setSpeed
------------------------------------------------------

.. function:: void OvenMediaPlayer::setSpeed(float speed)

	재생 속도를 조절합니다. 0.5배속 (2배 느리게) 부터 2배속 (2배 빠르게) 사이에서 속도를 지정할 수 있습니다.

	:rtype: void
	:param float speed: 속도 : 범위(0.5 ~ 2.0) 

seekTo
------------------------------------------------------
.. function:: void OvenMediaPlayer::seekTo(int sec)

	현재 재생 중인 미디어를 지정한 위치로 이동하는 기능이며, 로컬 파일 및 VoD 스트림을 재생할 때 사용할 수 있습니다. Live 스트리밍을 재생 할때는 동작하지 않습니다.

	:rtype: void
	:param int sec: 이동할 위치 (초)

isPlaying
------------------------------------------------------
.. function:: boolean OvenMediaPlayer::isPlaying()

	현재 플레이어가 재생중인지 체크합니다.

	:rtype: boolean
	:return: 
		- true : 재생중
		- false : 일시 중지 / 중지 / 버퍼링 등의 상태

getDuration
------------------------------------------------------
.. function:: int OvenMediaPlayer::getDuration()

	현재 재생 중인 미디어의 총 재생 시간을 구합니다. 로컬 파일, VoD같은 경우에는 초단위로 값이 반환되며, Live 영상인 경우에는 0을 반환합니다.

	:rtype: int
	:return: 
		- > 0 : 로컬 파일, VoD 스트림 영상의 재생 시간 (초)
		- = 0 : Live 영상

getCurrentPosition
------------------------------------------------------
.. function:: int OvenMediaPlayer::getCurrentPosition()

	현재 미디어의 재생 위치를 구합니다.

	:rtype: int
	:return: 현재 재생 위치(초)

setScreenMode
------------------------------------------------------
.. function:: void OvenMediaPlayer::setScreenMode(int mode)

	영상 출력 모드를 설정합니다. 영상 비율 기준으로 출력하거나 화면 비율 기준으로 출력할 수 있습니다.

	:param int mode:
		- OVEN_SCREEN_NORMAL(0) : 영상 비율 기준 (기본값)
		- OVEN_SCREEN_NOASPECTRATIO_FULL(1) : 화면 비율 기준
	:rtype: void

getStatus
------------------------------------------------------
.. function:: OvenPlaybackStatus OvenMediaPlayer::getStatus()

	현재 플레이어의 상태를 구합니다.

	:rtype: OvenPlaybackStatus
	:return: 플레이어 상태

	.. note::

		.. code-block :: java
			
			class OvenPlaybackStatus 
			{
				// 멈춤 
				public static final int OVEN_STATUS_STOP = 0;
				// 준비중
				public static final int OVEN_STATUS_PREPARING = 1;
				// 준비 완료
				public static final int OVEN_STATUS_PREPARED = 2;
				// 준비 실패
				public static final int OVEN_STATUS_PREPARED_FAILED = 3;
				// 재생중
				public static final int OVEN_STATUS_PLAY = 4;
				// 일시 중지
				public static final int OVEN_STATUS_PAUSE = 5;
				// 버퍼링 중
				public static final int OVEN_STATUS_BUFFERING = 6;
				// 재생 완료
				public static final int OVEN_STATUS_PBCOMPLETE = 7; 
			}

getMediaType
------------------------------------------------------
.. function:: OvenMediaType OvenMediaPlayer::getMediaType()

	현재 재생되고 있는 미디어의 종류를 구합니다. 

	:rtype: OvenMediaType
	:return: 미디어 종류

	.. note::

		.. code-block :: java
			
			class OvenMediaType
			{
				// 알 수 없음
				public static final int AM_MEDIA_UNKNOWN = 0;
				// 비디오
				public static final int AM_MEDIA_VIDONLY = 1;
				// 오디오
				public static final int AM_MEDIA_AUDONLY = 2;
				// 비디오 + 오디오
				public static final int AM_MEDIA_AVBOTH = 3;
			}



getStreamType
------------------------------------------------------
.. function:: OvenStreamType OvenMediaPlayer::getStreamType()

	재생하고 있는 스트림 종류를 구합니다. VoD 와 LIVE 를 구분할 수 있습니다. 

	:rtype: OvenStreamType
	:return: 스트림 종류

	.. note::

		.. code-block :: java
			
			class OvenStreamType
			{
				// 스트림 종류를 판별할 수 없음
				public static final int OVEN_STREAM_NONE = 0;
				// 로컬 파일 또는 VoD 스트림
				public static final int OVEN_STREAM_VOD = 1;
				// 라이브 스트림
				public static final int OVEN_STREAM_LIVE = 2;
			}

getScreenOnWhilePlaying
------------------------------------------------------
.. function:: void OvenMediaPlayer::setScreenOnWhilePlaying(Boolean screenOn)

	재생 중 장시간 사용자 입력이 없을 경우 화면 절전 모드로 진입하는 기능을 온오프 합니다.

	:rtype: void
	:param Boolen screenOn:
		- TRUE : 화면 켜짐 유지
		- FALSE : 화면 절전 모드 사용 (기본값)

setUserAgent
------------------------------------------------------
.. function:: void OvenMediaPlayer::setUserAgent(String userAgent)

	HLS 또는 HTTP Progressive Download 스트림을 요청할 때 HTTP 헤더에 UserAgent 값을 임의로 지정합니다.

	:rtype: void
	:param String userAgent: 사용자 정의 UserAgent 값

getUserAgent
------------------------------------------------------
.. function:: String OvenMediaPlayer::getUserAgent()

	HLS 또는 HTTP Progressive Download 스트림을 요청할 때 HTTP 헤더에 넣는 설정된 UserAgent 값을 구합니다.

	:rtype: String
	:return: 정의된 UserAgent 값

getDefaultUserAgent
------------------------------------------------------
.. function:: String OvenMediaPlayer::getUserAgent()

	시스템에 설정된 HTTP 헤더의 UserAgent 값을 구합니다.

	:rtype: String
	:return: 정의된 UserAgent 값

release
------------------------------------------------------
.. function:: void OvenMediaPlayer::release()

	플레이어에 할당된 모든 자원을 해제합니다. 플레이어를 더 이상 사용하지 않을 때 호출합니다.

	:rtype: void