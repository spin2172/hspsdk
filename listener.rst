.. raw:: pdf

   PageBreak

.. _listener:

======================================================
Event Listener 목록
======================================================
**OvenMediaPlayer** Class가 제공하는 Event Listener를 나열합니다.

.. _setInitCompleteListener:

setInitCompleteListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setInitCompleteListener(OvenInitCompleteListener l)
	
	플레이어 생성 후에 발생되는 초기화 완료 이벤트를 등록합니다.

	:rtype: 
		void
	:param OvenInitCompleteListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onInitComplete(OvenMediaPlayer i)

			OvenInitCompleteListener의 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스	
	
	``예제``

	.. code-block:: java

		OvenInitCompleteListener mInitCompleteListener = new OvenInitCompleteListener() 
		{
			public void onInitComplete(OvenMediaPlayer i){
				i.setDataSource("http://server.com/vod/playlist.m3u8");
				i.prepare();
			}
		};

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnInitCompleteListener(mInitCompleteListener);

.. _setOnPreparedListener:

setOnPreparedListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnPreparedListener(OvenPreparedListener l)
	
	prepare 함수를 호출 후에 발생되는 재생 준비 완료 이벤트를 등록합니다. 

	:rtype: 
		void
	:param OvenPreparedListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onPrepared(OvenMediaPlayer i, boolean result)

			OvenPreparedListener 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스
			:param boolean result: 준비 성공 여부
	
	``예제``

	.. code-block:: java

		OvenPreparedListener mPreparedListener = new OvenPreparedListener() 
		{
			public void onPrepared(OvenMediaPlayer i, boolean result) {
				Log.d("OvenPlayerLib", String.format("%s", success?"Success":"Failed"));
			}
		};

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnPreparedListener(mPreparedListener);


.. _setOnBufferingUpdateListener:

setOnBufferingUpdateListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnBufferingUpdateListener(OvenBufferingListener l)
	
	버퍼링 진행 상태 이벤트를 등록합니다.

	:rtype: 
		void
	:param OvenBufferingListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onBuffering(OvenMediaPlayer i, int percent)

			OvenBufferingListener 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스
			:param int percent: 버퍼링 진행률 (0 ~ 100)
	
	``예제``

	.. code-block:: java

		OvenBufferingListener mBufferingUpdateListener = new OvenBufferingListener() {
			public void onBuffering(OvenMediaPlayer i, int percent) {
				Toast.makeText(getApplicationContext(), 
				String.format("Buffering : %d%%", percent),
				Toast.LENGTH_SHORT).show();
			}
		};
		
		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnBufferingUpdateListener(mBufferingUpdateListener);

.. _setOnSeekCompleteListener:

setOnSeekCompleteListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnSeekCompleteListener(OvenSeekCompleteListener l)
	
	미디어 재생 위치 이동 완료 이벤트를 등록합니다.

	:rtype: 
		void
	:param OvenSeekCompleteListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onSeekComplete(OvenMediaPlayer i)

			OvenSeekCompleteListener 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스
	
	``예제``

	.. code-block:: java

		OvenSeekCompleteListener mSeekCompleteListener = new OvenSeekCompleteListener() {
			public void onSeekComplete(OvenMediaPlayer i) {
				Toast.makeText(getApplicationContext(), 
				String.format("Seek Completed"), 
				Toast.LENGTH_SHORT).show();
			}
		};
		
		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnSeekCompleteListener(mSeekCompleteListener);

.. _setOnErrorListener:

setOnErrorListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnErrorListener(OvenErrorListener l)
	
	플레이어에서 발생하는 에러를 onError 이벤트를 통해 전달 받을 수 있습니다. 미디어 재생 오류, 네트워크 문제, CPU 성능에 따른 디코딩 성능 부족 및 기타 에러가 발생하면 호출됩니다.

	:rtype: 
		void
	:param OvenErrorListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onError(OvenMediaPlayer i, int code)

			OvenErrorListener 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스
			:param int code: 
				- OvenErrorCode.OVEN_ERROR_OPEN_FAILED : 파일 열기 실패
				- OvenErrorCode.OVEN_ERROR_PREPARE_FAILED : 연결 실패
				- OvenErrorCode.OVEN_ERROR_PLAYBACK_FAILED : 재생 실패
				- OvenErrorCode.OVEN_ERROR_CODEC_FAILED : 알수없는 코덱
	``예제``

	.. code-block:: java

		OvenErrorListener mErrorListener = new OvenErrorListener() {
			public void onError(OvenMediaPlayer t, int code) {

				switch (code) {
				case OvenErrorCode.OVEN_ERROR_OPEN_FAILED:
					Log.d(TAG, String.format("Couldn't open file"));
					break;
				case OvenErrorCode.OVEN_ERROR_PREPARE_FAILED:
					Log.d(TAG, String.format("Couldn't find stream information"));
					break;
				case OvenErrorCode.OVEN_ERROR_PLAYBACK_FAILED:
					Log.d(TAG, String.format("Unstable network or unknown error"));
					break;
				case OvenErrorCode.OVEN_ERROR_CODEC_FAILED:
					Log.d(TAG, String.format("Couldn't find support codec"));
					break;
				}

				t.stop();
			}
		};
	
	public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
	mMediaPlayer.setOnErrorListener(mErrorListener);

.. _setOnCompletionListener:

setOnCompletionListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnCompletionListener(OvenCompletionListener l)
	
	미디어 재생 완료 이벤트를 등록합니다.

	:rtype: 
		void
	:param OvenCompletionListener l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onCompletion(OvenMediaPlayer i)

			OvenCompletionListener 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스

	``예제``

	.. code-block:: java

		OvenCompletionListener mCompletionListener = new OvenCompletionListener() {
			public void onCompletion(OvenMediaPlayer i) {
				Toast.makeText(getApplicationContext(),	
				String.format("Streaming playback is completed"), 
				Toast.LENGTH_SHORT).show();
				
				mMediaPlayer.stop();
				mMediaPlayer.prepare();
			}
		};

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnCompletionListener(mCompletionListener);


.. _setOnTimedMetatdataUpdateListener:

setOnTimedMetatdataUpdateListener
------------------------------------------------------
.. function:: void OvenMediaPlayer::setOnTimedMetadataUpdateListener(OvenTimedMetadateUpdated l)

	
	HLS Timed Meta 출력 이벤트를 등록합니다.

	:rtype: void
	:param OvenTimedMetadateUpdated l: 
		초기화 이벤트를 받을 리스너
	:인터페이스:
		.. function:: void onTimedMetadataUpdate(OvenMediaPlayer i, String m)
			:noindex:

			OvenTimedMetadateUpdated 인터페이스입니다.

			:rtype: void
			:param OvenMediaPlayer i: 플레이어 인스턴스
			:param String m: 메타데이터

	``예제``

	.. code-block:: java

		OvenTimedMetadataUpdatedListener mTimedMetaDataListener =
			new OvenTimedMetadataUpdatedListener() {
			public void onTimedMetadataUpdate(OvenMediaPlayer t, String meta) {
				Log.d(TAG, String.format("TimedMeta : %s", meta));
			}
		};

		public OvenMediaPlayer mMediaPlayer = new OvenMediaPlayer(this); 
		mMediaPlayer.setOnTimedMetadataUpdateListener(mTimedMetaDataListener);	