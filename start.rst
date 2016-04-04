.. raw:: pdf

   PageBreak

.. _start:

======================================================
간단한 예제
======================================================

OvenMediaPlayer 객체를 생성하고 이벤트 리스너를 등록하는 간단한 예제입니다.

플레이어 생성
------------------------------------------------------
OvenMediaPlayer를 멤버 변수로 선언하고 다음과 같이 초기화 하면 플레이어를 생성할 수 있습니다.

.. code-block:: java

	import com.airensoft.android.ovenmediaplayer.*;

	private OvenMediaPlayer mMediaPlayer = null;

	public void initMediaController(){ 
		mMediaPlayer = new OvenMediaPlayer(this);
		mMediaPlayer.setInitCompleteListener(mInitCompleteListener);
		mMediaPlayer.setOnPreparedListener(mPreparedListener);
		mMediaPlayer.setOnErrorListener(mErrorListener);
		mMediaPlayer.setOnCompletionListener(mCompletionListener);
		mMediaPlayer.setOnBufferingUpdateListener(mBufferingUpdateListener);
		mMediaPlayer.setOnSeekCompleteListener(mSeekCompleteListener);
		mMediaPlayer.setDisplayChangeListener(mDisplayChangeListener);
		mMediaPlayer.setOnLogListener(mLogListener);
		mMediaPlayer.setSystemLogDisable(false);
		mMediaPlayer.setScreenOnWhilePlaying(true);
		mMediaPlayer.setAllowBackgroundTask(false);
		mMediaPlayer.setOnTimedMetadataUpdateListener(mTimedMetaDataListener);
	}

이벤트 리스너 정의
------------------------------------------------------
다음과 같이 이벤트 리스너를 정의하여 사용하면 플레이어 이벤트를 처리할 수 있습니다.

.. code-block:: java

	// * 라이브러리 초기화 리스너
	OvenInitCompleteListener mInitCompleteListener = new OvenInitCompleteListener() {
		public void onInitComplete(OvenMediaPlayer t) {
			Log.d(TAG, String.format("Initialize Complete"));				
			// 플레이어 상태 초기화
			t.reset();
		}
	};

	
	// 준비 완료 이벤트 리스너
	OvenPreparedListener mPreparedListener = new OvenPreparedListener() {
		public void onPrepared(OvenMediaPlayer t, boolean result) {
		
			// Preparing이 성공하면 자동으로 재생함
			if(result==true)
			{
				Log.d(TAG, String.format("Video Resolution: %d/%d", 
				mMediaPlayer.getVideoWidth(), mMediaPlayer.getVideoHeight()));
				mMediaPlayer.start();
			}
		}
	};

	// * 버퍼링 업데이트 이벤트 리스너
	OvenBufferingListener mBufferingUpdateListener = new OvenBufferingListener(){
		public void onBuffering(OvenMediaPlayer t, int percent) {
			Toast.makeText(getApplicationContext(), 
			String.format("%d%%", percent), Toast.LENGTH_SHORT).show();
		}
	};

	// * SEEK 완료 이벤트 리스터
	OvenSeekCompleteListener mSeekCompleteListener = new OvenSeekCompleteListener() {
		public void onSeekComplete(OvenMediaPlayer t) {
			Toast.makeText(getApplicationContext(), 
			String.format("Seek Completed"), Toast.LENGTH_SHORT).show();
		}
	};
	
	// * 에러 이벤트 리스너
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
	
	// * 동영상 재생 완료 이벤트 리스너
	OvenCompletionListener mCompletionListener = new OvenCompletionListener() {
		public void onCompletion(OvenMediaPlayer t) {
			Toast.makeText(getApplicationContext(),	
			String.format("completed"), Toast.LENGTH_SHORT).show();
			
			mMediaPlayer.stop();
			mMediaPlayer.prepare();
		}
	};


Surface 할당
------------------------------------------------------
비디오 출력을 위한 Surface View의 Surface Holder를 플레이어에 할당해줍니다.

.. code-block:: java

	mVideoView = (SurfaceView) findViewById(R.id.surfaceView1);
	mVideoView.getHolder().addCallback(new SurfaceHolder.Callback() {
		@Override
		public void surfaceChanged(SurfaceHolder holder, int format, 
									int width, int height) {
			// * Surface뷰가 변경되면 SurfaceHolder를 등록해줌			
			mMediaPlayer.setDisplay(holder);
		}
		@Override
		public void surfaceCreated(SurfaceHolder holder) {
			Log.e(TAG, "surfaceCreated");
		}
		@Override
		public void surfaceDestroyed(SurfaceHolder holder) {
			Log.e(TAG, "surfaceDestroyed");
			mMediaPlayer.clearDisplay();
		}
	});


재생, 일시정지 및 중지
------------------------------------------------------
기본적인 비디오 제어는 다음과 같은 방식으로 쉽게 연결할 수 있습니다.

.. code-block:: java

	// 일시정지
	mediaPlayer.pause();
	// 재생
	mediaPlayer.start();
	// 중지
	mediaPlayer.stop()

샘플 코드 다운로드
------------------------------------------------------
다음 URL에서 샘플 코드를 다운로드 할 수 있습니다.

https://github.com/AirenSoft/OvenPlayer-SDK-for-Android/sample